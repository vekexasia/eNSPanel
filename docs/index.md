# Welcome to eNSPanel

For full documentation visit [here](https://enspanel-docs.andreabaccega.com/).

## Features

* LD2410 presence sensor
* Microphone for voice assistant
* Mother-daughter pcb (to extend functionalities)
* enclosure compatibility `*`
* all the goodies from the NSPanel such as:
  * capacitive display
  * buzzer 
  * 2 relays
  * ...


`*` only if not slotting the LD2410. otherwise a 3d printed part is required.


## Why?

The NSPanel from Sonoff is a great device. I have 8 in my home serving as thermostats and doing much more. Unfortunately their outdated hardware is quite limiting. 

For example one of the reason why the ESPHome version struggles in **uploading the TFT** to the Nextion panel is the lack of free memory.

Another reason why the NSPanel needed an upgrade was/is the **lack of other functionalities.** With edge AI and wake-word recognition inside the ESP32-S3 module you could really have a **smart voice assistant in each room** (like I have in my case).

Initially I also wanted to slot a ZigBee module that could also enhance my home ZigBee network but starting from v1.4 I decided that mother-daughter approach was the best to minimize costs and reduce waste.

For example one could design a daughter board with a small speaker to engage with the voice assistant... Want an atmospheric sensor? design a board for it. Not happy with the AI capabilities of the slotted ESP32-S3? you get the idea :)

  
