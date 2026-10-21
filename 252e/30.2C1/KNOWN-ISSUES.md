# Known issues and behaviour that is unchanged from Buchla's 30.2

## Not yet run on hardware
This candidate has been checked in the lab only and has never run on a module. Items listed under "Not yet run on hardware" in
the [release notes](RELEASE-NOTES.md) are still to be completed.

## A very hard spin is thinned out, and can step the wrong way
The fix keeps the knobs working during a fast spin, but it still limits how many steps a knob can deliver: a spin faster than about
140 steps per second delivers roughly 140–215 steps per second rather than every step. With worn or noisy contacts, an extremely
fast flick can also produce an occasional step in the wrong direction. Normal turning is unaffected.

## Two knobs together
Two knobs turned at the same time still share one reader, so each loses some steps (fewer than before, but not none).

## Most buttons have no debounce
Fifteen of the 21 panel buttons act on every contact change. Because their actions toggle, a bounce can cancel a tap, and on the
hold buttons a bounce can trigger the short-press action early. Unchanged.

## Waits on the bus
Several bus transfers wait with no time limit, and the hardware watchdog remains off, as in 30.2. A stuck bus can freeze the module
until power-cycle. Long operations (preset SAVE, BACKUP) can drop panel events while they run.

## Version information
The module reports **30.2C1**. The firmware-card image header still reads 30.2 (cosmetic).

## Release candidate
This is release candidate 1.
