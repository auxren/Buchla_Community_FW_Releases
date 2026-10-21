# 200e Bus Buccaneer — alpha 1

A Mac app that updates the firmware of your 200e modules through a Xenomorpher, so you do not need Buchla's USB Firmware Card and
a computer running Buchla's utility. It reads a signed list of firmware (this repository's `catalog.json`), shows you what your
modules report on the bus, and walks you through the update.

**Status: alpha. Not yet run on hardware.** Nothing in this alpha has been run against a real Xenomorpher, bus or module yet.
Alpha 1 is published for owners who can test with its author present, so that a problem can be caught and fixed on the spot. Expect rough edges; read [INSTALL.md](INSTALL.md) first.
The catalog it reads is signed with a **development key** for now, so this alpha build and this catalog belong together; a later
build will switch to the release key.

## What it does
- Finds the Xenomorpher over USB and shows its name and firmware. It needs the Xenomorpher firmware build that ships alongside this
  app on its release page; the app checks the version and tells you if it is too old.
- Scans the 200e bus and lists each module with its model and the version it reports.
- Offers the community firmware for the module you pick (and Buchla's own versions it recognises, so it can tell you what a module
  is running). Each firmware file from the list is checked against its published checksum before anything is sent. A file you
  open yourself has no published checksum: if it is not a Buchla release the app recognises, the app asks you to confirm before
  it loads it, and it refuses a file made for a different model than the module you picked.
- Takes a backup of the module's presets before it writes anything, when the module has presets.
- Sends the firmware to the Xenomorpher, then tells you exactly when to power the case off, which button to hold and for how long.
- Shows the card being read while the module programs itself, then asks you to have the module report its version and tells you
  whether it matches.
- Works from a cached copy of the list when you are offline, and refuses a list whose signature does not check.

## What is not in it
- **Modules with an AVR32 processor** (251e, 252e, 218e and similar) are not supported on this route yet. The app lists them but will not
  write to them.
- **Studio H 2WIRELESS (WPM) over Wi-Fi** is not supported in this alpha.
- **Preset management** (browsing, restoring, editing banks) is not in this alpha; the pre-update backup is saved to disk but the
  app cannot restore it yet.
- **Windows** is not available yet; this alpha is for macOS.
- Modules marked "not yet run on hardware" in this repository's [README](../README.md) are offered with that warning.
- Modules whose entry in the app has not been confirmed on hardware can be updated only after you tick a box saying you understand
  that. A module whose load button is not known is listed but not offered for an update.

## Known limits
- Updating is only attempted when the Xenomorpher reports that it supports firmware transfer; otherwise the app asks you to update
  the Xenomorpher first.
- The app never writes while a WPM is on the bus; unplug it first.
- A module that does not come back is power-cycled, not retried; the app says so rather than guessing.

Reports from anyone who tries it are welcome.
