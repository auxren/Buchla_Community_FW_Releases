# WPM firmware 1.19

Community firmware for the Buchla WPM (the Wi-Fi preset manager), built from the open-source
2WIRELESS project, version 1.19. Everything the WPM did in 1.18 is unchanged: the web page, the
preset pages and the memory routes behave exactly as before.

## What is new

- **Updates over Wi-Fi.** Once 1.19 is on the WPM, later versions can be sent to it over Wi-Fi by the
  200e Bus Buccaneer app. The WPM checks the new image before it switches to it and keeps running the
  old one if the check fails.
- **Reports its version.** The WPM now answers a version request, so the app can tell what it is
  running and whether an update applies.
- **Web interface fix.** Fixes a case where the WPM's web interface stopped answering.

## Files

- `wpm-1.19.ino.bin` — the full image. Use this for the first install from 1.18, or for recovery: it is
  sent over the WPM's USB port by the app (or by the Arduino tools) and replaces everything.
- `wpm-1.19.ota.bin` — the Wi-Fi image. The app sends this over Wi-Fi to a WPM that already runs 1.19 or
  later. It cannot be used for the first install.
- `SHA256SUMS` — checksums of both. The app checks a file against these before it sends it.

## Installing from 1.18

The stock 1.18 firmware cannot receive an update over Wi-Fi, so the first install uses the WPM's USB
port. Unplug the WPM from the case, connect it to the Mac by USB, and follow the app's "Update the WPM
over USB" steps. If a USB install is interrupted, the WPM stays in its built-in bootloader; the app
recognises that state and offers to send the full image again.
