# WPM firmware 1.21

Community firmware for the Buchla WPM, built from the open-source 2WIRELESS project, version 1.21.
Everything 1.20 did is unchanged; this release adds a preset capture that works for every module,
including the ones the stock firmware could not back up. The work is submitted upstream as
[studiohsoftware/2WIRELESS pull request 7](https://github.com/studiohsoftware/2WIRELESS/pull/7),
stacked on the 1.19 and 1.20 ones.

## What is new

- **Preset capture for every module.** The app can ask the WPM to back up one module's presets and
  watch the capture as it happens: how many bytes have arrived, whether the module has finished, and
  whether anything was missed. Modules that start sending late, or send a lot (the 251e sends about
  63 KB), are captured completely. The result is laid out exactly as a capture through a Xenomorpher,
  so the two can be compared byte for byte.
- **Nothing else touches the bus during a capture or a scan.** While either runs, the WPM's other
  bus-facing functions answer "busy" instead of interrupting it, and MIDI arriving over USB is held
  back.
- **Remote control stays yours.** The WPM never switches a module's remote control on by itself;
  the app asks you first when a module needs it (the 251e does).
- **Reports what it can do.** The version answer now lists "dump" alongside "version", "ota" and "bus".

Reading memory back from the WPM is a little slower in this release (a firmware update's check takes
about half a minute instead of twenty seconds). Sending is unchanged.

## Files

- `wpm-1.21.ino.bin` — the full image, for a first install or recovery over the WPM's USB port.
- `wpm-1.21.ota.bin` — the Wi-Fi image. The app sends this over Wi-Fi to a WPM that already runs 1.19
  or later. It cannot be used for the first install.
- `SHA256SUMS` — checksums of both. The app checks a file against these before it sends it.

## Installing

From 1.19 or later: the app updates the WPM over Wi-Fi. From stock 1.18: install over USB first (see
the 1.19 notes), or install this version over USB directly.
