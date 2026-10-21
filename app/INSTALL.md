# Installing 200e Bus Buccaneer (alpha 1)

**Before you start:** the app changes the firmware of a module. Take your own backup of anything you cannot lose, and keep Buchla's
own firmware for the module on hand so you can go back. The app saves a backup of a module's presets before an update, but alpha 1
cannot restore it for you.

## What you need
- A Mac running macOS 13 or newer.
- A **Xenomorpher** connected to your computer by USB and to the 200e bus, running a firmware recent enough to support firmware
  transfer. If yours is too old, the app tells you to update the Xenomorpher first and shows the version it needs.
- A module with an 8051-family processor (most 200e modules). **AVR32 modules (251e, 252e, 218e and similar) are not supported on
  this route yet.** The app will not write to them.
- **No Studio H 2WIRELESS (WPM) on the bus.** The bus has one firmware card address and the WPM uses it; unplug the WPM while you
  update, then plug it back in.

## Install
1. Download the app's disk image from this repository's releases and open it.
2. Drag **200e Bus Buccaneer** into Applications and open it.
3. The first time, the app downloads the firmware list from this repository and checks its signature. With no network it uses the
   copy it saved last time.

## The three screens
- **Connect:** shows the Xenomorpher it found (name, firmware) and the modules on the bus with the version each one reports.
- **Update:** choose a module and a firmware. The app lists what will happen, backs up the module's presets, sends the firmware to the
  Xenomorpher, and then guides you through the power-cycle step. It shows the card being read, then checks the version the module
  reports afterwards.
- **Settings:** where backups are kept and which firmware list the app reads.

## The power-cycle step
The module only loads new firmware when it is powered on while its load button is held. When the app says the firmware is ready:
1. Power the whole case off.
2. Hold the button the app names for your module (Remote Enable on most; DATA or Clock on a few).
3. Power on, and keep holding until the module's lights come up, then let go.
4. Wait while the app shows the card being read. Do not power off until it says the module has finished.
5. When asked, hold the module's button so it reports its version. The app compares it with the firmware you chose.

If the module does not report the new version, the app says so. Power-cycle the module and try again, or go back to the firmware you
had before; each release's notes say how.

## Verify and go back
Every firmware file is checked against its published checksum before it is sent. To go back to a previous version, choose it in the
Update screen the same way, or use Buchla's own USB Firmware Card route described in each release's `INSTALL.md`.

**Never program a module's chip directly with a debug adapter**; see the top-level README.
