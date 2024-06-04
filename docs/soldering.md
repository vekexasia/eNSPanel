# Soldering

First component that needs to be soldered is the **ESP32**. This makes the first flashing super easy.

## ESP32 Soldering

A bare minimal component soldering includes:
- R9 (0603 10kΩ)
- C6, C2, C4, C3 (0603 100nF)
- C10, C12, C13 (0805 22uF)
- LDO (U4)

The components are circled here:

![esp32-soldering](images/esp32-soldering.png)
 
After soldering the ESP32, the LDO and the capacitors, the ESP32 can be flashed using the bottom right header. 


## LD2410 sensor soldering

Several iterations of the PCB were done to try to slot the LD2410 sensor without the need to change anything about the enclosure. Unfortunately, the sensor is too big to fit in the enclosure.

The best compromise was to have the sensor laying on top of the PCB. This way there is a semi-easy way to solder the LD2410 sensor.

To do that:

- place the sensor on the PCB.
- fill the pins with solder paste,
- use a hot air gun.