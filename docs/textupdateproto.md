## The problem

My specific setup is a Home Assistant integration with ESPHome.

The Nextion firmware has more than 15 text elements that rely on home assistant for their content.

The "original" way of updating the text elements is to use the `text_sensor` component in ESPHome and update the text elements in the Nextion firmware using the `on_value` trigger.

But this approach **requires a `text_sensor` per component** hence the code becomes a mess really fast...

The solution involves 2 parts:

- **Home Assistant side**: a text sensor that holds all the text elements in a single string
- **ESPHome side**: a script that parses the string and updates the text elements in the Nextion display

It's important to note that this approach **can be used standalone** and there is nothing in this project that relies on this approach/protocol.

I just found it useful for my specific use case. So documenting it here sounds like a good idea.

## The protocol

To fix my issue I had to invent a text format that could be easily parsed by the ESPHome script(see below) and HomeAssistant printable.

One caveat I found is that text sensor in Home Assistant does not support states longer than 255 characters. So I used an attribute instead.

The text format is as follows:

```
$page.$componentName,$value|
$page.$componentName,$value|
|
```

- `$page`: is the page name in the Nextion display
- `$componentName`: is the component name in the Nextion display
- `$value`: is the value to be set in the text component

Between each component there is a `|\n` separator. The end is marked by a `|` character.

## EspHome side

```yaml
script:
  - id: restore_nspanel_texts
    then:
      - lambda: |-
          std::string main = id(nspanel_texts).state;   
          std::string md = "| ";   

          size_t pos = 0;   
          int index = 0;   
          while ((pos = main.find(md)) != std::string::npos) {   
            std::string s = main.substr(0, pos);   
            main.erase(0, pos + md.length());  
            std::string delimiter = ",";   
            std::string key = s.substr(0, s.find(delimiter));   
            std::string value = s.substr(key.length() + 1, s.rfind(delimiter) - key.length()  - 1); 
            id(disp1).set_component_text_printf(key.c_str(), "%s", value.c_str());
          }

text_sensor:
  - platform: homeassistant
    id: nspanel_texts
    entity_id: sensor.nspanel_texts
    attribute: value
    on_value:
      then:
        - script.execute: restore_nspanel_texts

```

## Home Assistant side

Home assistant side obviously depends on your personal setup both in HA and Nextion.

Anyways here is a simple example of how to create such sensor.

```yaml
template:
  - sensor:
    - name: "NSPanel Texts"
      state: >-
        {{ now().strftime('%d-%m-%Y %H:%M:%S') }}
      attributes:
        value: >-
          weather_now.temp_out,{{states('sensor.nspanel_outside_temp')}}|
          weather_now.humidity_out,{{states('sensor.nspanel_outside_humidity')}}|
          weather_now.wind_speed,{{states('sensor.nspanel_outside_windspeed')}}|
          weather_now.sunset,{{states('sensor.nspanel_next_sunset')}}|
          weather_now.sunrise,{{states('sensor.nspanel_next_sunrise')}}|
          |
```

This is a simple example of how to update the weather information in the Nextion display updating the `weather_now` page components.
