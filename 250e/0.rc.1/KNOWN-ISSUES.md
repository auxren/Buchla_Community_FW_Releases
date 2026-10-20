# Known issues and behaviour that is unchanged from Buchla's 30.6b1

## Not yet run on hardware
This release candidate has not been flashed to a module. It was checked in the lab only. The first thing to find out on a
real 250e is whether the encoder behaves cleanly at slow speed after this change (see the next item) and whether fast
flicks now move the cursor or value by the right number of steps.

## Encoder contact bounce
Looking at the encoder more often also lets the module see electrical bounce of the encoder contacts, which the old, slower
look mostly hid. A bounce on the edge of a detent normally nets out (a step forward, back, forward), but it may show as a
brief flicker of the stage cursor during a slow single-detent turn. If you see that, please report it with the encoder's
make if known; a small filter can be added in a later release.

## Encoder is blind during card transfers and preset saves
While the module is writing a preset or running a card BACKUP / RESTORE, it cannot read the encoder. Turning the knob during
those operations still loses steps. This is unchanged from Buchla's firmware.

## Panel can freeze if the bus master stops acknowledging
If another device on the 200e bus stops answering while the module is waiting for it, the module can hang with dead knobs
and buttons until a power cycle. This is Buchla's original behaviour and is unchanged in this release.

## Card BACKUP / RESTORE waits
The card transfer routines wait for the card with no time limit and run with the module's other activity paused, as in
Buchla's firmware. A card that stops responding mid-transfer can freeze the module.

## Short button taps
Buttons are debounced over a few milliseconds (about 30 ms for the long-press button). Taps shorter than that are ignored.
This is unchanged.

## Base firmware is a beta
30.6b1 is a Buchla beta release. Beyond the encoder fix, this release contains exactly what that beta contains, including
anything Buchla later changed or may change.

## Version information
The module reports **0.rc.1**. The firmware-card image header still reads 30.6b1 (cosmetic).

## Release candidate
This build has not run on hardware; see the [release notes](RELEASE-NOTES.md).
