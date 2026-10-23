# WPM firmware 1.20

Community firmware for the Buchla WPM, built from the open-source 2WIRELESS project, version 1.20.
Everything 1.19 did is unchanged; this release adds a bus scan the 200e Bus Buccaneer app can ask for.
The work is submitted upstream as a pull request on the 2WIRELESS project, stacked on the 1.19 one.

## What is new

- **Bus scan.** The app can ask the WPM which modules are on the bus. The WPM queries each address in
  turn and reports the ones that answer. A full sweep takes about 50 seconds; checking one address
  takes about two. A module's version appears only when the module has announced it (hold its button)
  or the WPM already holds it; otherwise the scan shows the module without a version.
- **Scans wait for a quiet bus.** A scan is refused for a moment right after a module has been reading
  its presets from the WPM, and each query waits for the bus to go quiet, so a scan cannot interrupt a
  module that is still loading.
- **Reports what it can do.** The WPM's version answer now lists "bus" alongside "version" and "ota",
  so the app knows the scan is available.

## Files

- `wpm-1.20.ino.bin` — the full image, for a first install or recovery over the WPM's USB port.
- `wpm-1.20.ota.bin` — the Wi-Fi image. The app sends this over Wi-Fi to a WPM that already runs 1.19
  or later. It cannot be used for the first install.
- `SHA256SUMS` — checksums of both. The app checks a file against these before it sends it.

## Installing

From 1.19 or later: the app updates the WPM over Wi-Fi. From stock 1.18: install over USB first (see
the 1.19 notes), or install this version over USB directly.
