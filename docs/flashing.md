# Flashing

After [slotting](/soldering) the ESP32 along with the first required components, you **do not need to solder the header**. Actually it's not a good idea also because the display will not fit anymore and desoldering it is a pain..

I would recommend to either use some pogo pin clips like [this one](https://aliexpress.com/item/1005004869027755.html), or just press fit the pins keeping them in place.

After the first flashing, the other components can be soldered in any order.

## Flashing the Firmware

Besides the hardware connection you need to either use the [esphome cli](https://esphome.io/guides/getting_started_command_line.html) or the [web esphome](https://web.esphome.io/) flasher using a USB-TTL adapter.

To enter bootloader mode you need to connect the `EN` and `IO0` pins to ground. Specifically I find that a good way to to it is following the sequence below:

- Connect your adapter to the header provided
- Connect the `EN` pin to ground
- Connect the `IO0` pin to ground
- Remove the `EN` pin from ground
- Remove the `IO0` pin from ground

**PROTIP**: The ESP32 metal case is GND.

## The First Firmware
As per the first firmware the following should just work out of the box.

```yaml
esphome:
  name: sample-esp32
  friendly_name: sample-esp32
  platformio_options:
    board_build.flash_mode: dio
esp32:
  board: esp32-s3-devkitc-1
  framework:
    type: esp-idf

psram:
  mode: octal
  speed: 80MHz

# Enable logging
logger:
  hardware_uart: UART0
  level: DEBUG

# Enable Home Assistant API
api:
  # Once onboarded into HA u can remove this
  reboot_timeout: 0s
  encryption:
    key: "redacted"

ota:
  password: "redacted"

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
  # had issues with output_power not being specified
  output_power: 12dB
```

Flashing the previous bare minimum firmware should be straightforward. If you have any issues please refer to the [ESPHome documentation](https://esphome.io/guides/getting_started_command_line.html).
