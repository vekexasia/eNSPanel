Much like the original PCB, eNSPanel is slotting 2 microswitches to make a use of the 2 physical buttons.

## GPIO

The 2 microswitches are connected to the ESP32 via `IO42`(left) and `IO41`(right).

## Configuration

The most up-to-date configuration is in the `esphome` folder. This is a known to be working minimal configuration for the thermistor:

```yaml
binary_sensor:
  # Left button below the display
  - platform: gpio
    name: $friendly_devicename Left Button
    pin:
      number: GPIO42
      inverted: true
    id: left_button

  # Right button below the display
  - platform: gpio
    name: $friendly_devicename Right Button
    pin:
      number: GPIO41
      inverted: true
    id: right_button

```

