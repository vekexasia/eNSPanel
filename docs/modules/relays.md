Much like the original PCB, eNSPanel supports the original 2 Relays.

Furthermore, even if there is no use for them right now, there are 2 other GPIO pins that can be used in the future in case there will ever a need for a new pcb for the power supply module.
## GPIO

The 2 relays are connected to the ESP32 via `IO11` and `IO12`.

## Configuration

The most up-to-date configuration is in the `esphome` folder. This is a known to be working minimal configuration for the 2 relays:

```yaml
switch:
  # Physical relay 1
  - platform: gpio
    name: Relay 1
    id: relay_1
    pin:
      number: 11
  # Physical relay 2
  - platform: gpio
    name: Relay 2
    id: relay_2
    pin:
      number: 12
```


# Climate configuration

As explained in the [thermistor](thermistor.md) documentation, the ESPHome platform provides a [climate component](https://esphome.io/components/climate/index.html) that can be used to control a heater or a cooler. The climate component can be used to control a relay that turns on a heater or a cooler. 

The following is a sample configuration to leverage one of the relay to control a heater:

```yaml
climate:
  - platform: thermostat
    id: termostato
    name: "Termostat"
    sensor: temperature
    min_heating_off_time: 60s
    min_heating_run_time: 60s
    min_idle_time: 30s
    heat_action:
      - switch.turn_on: relay_1
    idle_action:
      - switch.turn_off: relay_1
    default_preset: Home
    preset:
      - name: Home
        default_target_temperature_low: $target_temp_home
        mode: HEAT
      - name: Comfort
        default_target_temperature_low: $target_temp_comfort
        mode: HEAT
```
