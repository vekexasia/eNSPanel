Much like the original PCB, eNSPanel uses an NTC thermistor to measure ambient temperature.

The thermistor is connected to the ESP32 via a voltage divider. The voltage divider is made up of a 20k resistor and the thermistor. The voltage divider is connected to the ESP32's ADC pin.

The thermistor is a normal 10k NTC thermistor with a B value of 3950. There is another 10k resistor in series with the thermistor to protect the ESP32's ADC pin.

## GPIO

The thermistor is connected to the ESP32 via `IO9` which is ADC1 in the selected ESP32 module.

## Configuration

The most up-to-date configuration is in the `esphome` folder. This is a known to be working minimal configuration for the thermistor:

```yaml
sensor:
  # Internal temperature sensor, adc value
  - platform: adc
    id: ntc_source
    pin: 9
    update_interval: 10s
    attenuation: auto

  # Internal temperature sensor, adc reading converted to resistance (calculation)
  - platform: resistance
    id: resistance_sensor
    sensor: ntc_source
    configuration: UPSTREAM
    resistor: 20kOhm
    

  # Internal temperature sensor, resistance to temperature (calculation)
  - platform: ntc
    id: temperature
    sensor: resistance_sensor
    calibration:
      b_constant: 3950
      reference_temperature: 25°C
      reference_resistance: 20kOhm
    name: Temperature
    filters:
      - median:
          window_size: 10
          send_every: 5
          send_first_at: 5

```

As you can see the termistor is read and averaged to avoid noise.

Also the ESPHome platform provides a [climate component](https://esphome.io/components/climate/index.html) that can be used to control a heater or a cooler. The climate component can be used to control a relay that turns on a heater or a cooler. Check the [relays](relays.md) documentation for more info.
