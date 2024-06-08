# Soldering

First component that needs to be soldered is the **ESP32**. This makes the first flashing super easy.

## 1) ESP32 Soldering

A bare minimal component soldering includes:
- R9 (0603 10kΩ)
- C6, C2, C4, C3 (0603 100nF)
- C10, C12, C13 (0805 22uF)
- LDO (U4)

The components are circled here:

![esp32-soldering](images/esp32-soldering.png)
 
After soldering the ESP32, the LDO and the capacitors, the ESP32 can be flashed using the bottom right header. 

## 2) Other modules

The other modules can be soldered in any order. Just make sure to follow the schematic and the BOM.
I'd recommend to [flash first](flashing.md) the ESP32 and then solder the other components.

Some modules might be tricky to solder. For example, the [microphone](modules/microphone.md) and the [LD2410](modules/presence.md) might require some patience.

I'd solder the bottom layer components after first flashing the ESP32. This way you can test the ESP32 and the LDO. 
