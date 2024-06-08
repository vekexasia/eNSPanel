## Soldering

Most of the time soldering the right components properly is the key to a successful build. Check the [soldering](soldering.md) page for more info.

Especially the microphone and the LD2410 might be tricky to solder.

## Bootloop

It happened to me that the ESP32 went into a bootloop after being flashed with a minimal firmware.

I am not sure what caused it, but I suspect it was the `output_power` not being specified in the `wifi` section as adding it fixed the issue.

## Microphone not recognizing wake word

If the microphone is not recognizing the wake word, it might be due to the microphone not being properly soldered.

## LD2410 not working

If the LD2410 is not working, it might be due soldering issue. Check the soldering and the connections. The [presence sensor](modules/presence.md) page shows a diagram of the connections.
