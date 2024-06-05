Since ESPHome supports on-device wake word detection, it is possible to use the wake word detection to trigger a voice assistant. This is a sample configuration that uses the wake word detection to trigger a voice assistant.

Considering the chosen module (ESP32-S3-WROOM-1-N16R8) has PSRAM, the eNSPanel is fully capable to perform on-device wake word detection.

After properly configuring the [microphone](modules/microphone.md), the following configuration can be used to trigger a voice assistant.

```yaml
esphome:
  on_boot:
    priority: -100
    then:
      - micro_wake_word.start:
external_components:
  - source: github://pr#5230
    components: esp_adf
    refresh: 0s
micro_wake_word:
  microphone: mic
  model: hey_jarvis
  on_wake_word_detected:
    - rtttl.play: 'beep:d=16,o=5,b=100:e6'
    - wait_until:
        not:
          rtttl.is_playing:
    - voice_assistant.start:
voice_assistant:
  on_client_connected:
    - micro_wake_word.start:
  on_client_disconnected:
    - micro_wake_word.stop:
  on_error:
    then:
      - rtttl.play: 'beep:d=16,o=5,b=100:e6'
  on_end:
    then:
      - wait_until:
          not:
            voice_assistant.is_running:
      - micro_wake_word.start:  
```

For debug purposes, once recognized, the buzzer will play a beep and the voice assistant will start. 
