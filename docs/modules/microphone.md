The microphone is one of the new features included in the eNSPanel PCB. 

I decided to slot a microphone cause I wanted to have a device in each room capable of recognizing a wake word.

## GPIO

The microphone needs to be a footprint compatible (see part below) i2c microphone. the following ESP32 pins were used:

- GPIO38 - lrclk
- GPIO40 - bclk
- GPIO39 - din

## Configuration

Always refer to the `esphome` folder for the most up to date working configuration. This is a known to be working minimal configuration for the microphone

```yaml

i2s_audio:
  i2s_lrclk_pin: GPIO38
  i2s_bclk_pin: GPIO40
microphone:
  - platform: i2s_audio
    id: mic
    adc_type: external
    i2s_din_pin: GPIO39
    pdm: false
    channel: left
voice_assistant:
  microphone: mic
  auto_gain: 31dBFS
#  noise_suppression_level: 2
```

## Part

`ICS-43434` microphone was used and known to be working with the PCB.

## Soldering

Soldering such mics require some patience. A good solder paste does wonders.

What I usually do is:

- Solder all the components and keep the mic as last 
- Apply solder paste (Better with a stencil)
- use hot air gun
- gently apply some force on top,
- test...

In case it does not work I desolder with the hot air gun and repeat.

## Related Parts

Only C5 (top layer) and R3 (bottom layer) are needed to make the microphone to work. 

## Testing the mic

Sometimes it might be a pain to test a working microphone. To date I don't know any method more effective than installing the voice assist package and try to speak the wake word.

Aka. You should really check out the [voice assistant](/voice) section of this documentation

### Debugging poor audio quality

Most of the times if u hear statics or other jibberish it means the microphone is not properly soldered onto the board.
