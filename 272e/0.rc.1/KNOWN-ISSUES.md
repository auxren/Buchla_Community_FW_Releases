# Known issues and behaviour that is unchanged from Buchla's 31.0b1

## Bus RECALL / SAVE / BACKUP / RESTORE need a "polling complete" message after power-up
This is Buchla's original behaviour and is **not** changed in 0.rc.1. The 272e only acts on RECALL, SAVE, BACKUP and RESTORE
received over the 200e bus once it has received the *polling complete* frame (`04 00 22 14 FF`) since power-up.
- The Remote-enable frame only lights the Remote LED; it does not allow these commands.
- The Remote button cannot allow them either until a polling-complete frame has been received.
- Buchla's Wireless Preset Manager sends polling-complete about 2 s after **its own** power-up when its *poll on start* setting is on.
- On a bus without a preset manager, the bus master must send it. The Xenomorpher firmware from Xenomorphicle commit `48938129` does this
  automatically about 8 s after boot when it sees no preset manager.
Without it, RECALL frames are received and silently ignored, and the Remote LED can still look lit.

## Remote LED
If no polling-complete has been received since power-up, the Remote LED can relight itself shortly after being turned off with the
Remote button. This is the original design and is unchanged.

## Waits that remain unbounded
Two waits in the card BACKUP / RESTORE routines (for the bus transfer-complete flag) are unchanged, because changing them could
not be done safely without further testing. The module's hardware watchdog remains disabled, as in 31.0b1.

## Panel responsiveness
The panel is much more responsive, but the module's processor is still mostly occupied by its fast panel-scanning routine, as in
31.0b1. That scanning was not redesigned in this release.

## Version information
The module reports **0.rc.1** (key code 22 and the bus announcement). The firmware-card image header still reads 31.0 (cosmetic).

## Release candidate
Items listed under "Not yet run on hardware" in the [release notes](RELEASE-NOTES.md) are still to be completed.
