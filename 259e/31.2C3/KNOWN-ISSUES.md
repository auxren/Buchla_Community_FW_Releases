# Known issues and behaviour that is unchanged from Buchla's 31.2

## Going back
If you prefer the old behaviour, power up holding SHAPE for Twisted; 31.2C2 (choice at every power-up) or Buchla's 31.2 can
be reflashed. The stored byte lives in the calibration area and is ignored by those builds.

## The memory for the choice is finite
Each change uses one byte of a 1008-byte area; after about a thousand changes the last choice stays and further holds no
longer change it (nothing else goes wrong). A firmware update does not clear it.

## Order of the original tables
The three original tables per side are assigned to a, b and c in the order they sit in the module's memory. The original
259e may have numbered them differently. If you know the original order, say so and it can be changed.

## Knobs stop a little short of full scale when swept upwards
Buchla's 31.2 keeps a small dead band on each knob so that noise and direction reversals do not jitter the parameter. A side
effect is that a knob swept upwards reads about 0.7 % below its true position. Unchanged because changing it changes the
knob feel.

## All 30 presets live in one flash block
Every SAVE rewrites the entire preset bank. A power loss during the save window loses all 30 presets. Buchla's original
design, unchanged. Keep a BACKUP of your bank. (The stored mode choice of 31.2C3 does not use this mechanism.)

## Card BACKUP / RESTORE waits
The card transfer routines still wait for the bus with no time limit, with the audio engine paused for the duration, as in
31.2. The hardware watchdog remains disabled, as in 31.2.

## Remote LED turns on by itself
After power-up or a preset recall, the first knob or button edit turns Remote Enable on if no preset manager has started
polling. Buchla's original behaviour, unchanged.

## Holding Remote saves to preset 0
Holding the Remote button for about 0.4 s (when no preset manager is polling) saves the current settings into preset slot 0
and re-initialises the bus interface. Buchla's original behaviour, unchanged. When a preset manager is polling, the same hold
sends the version announcement instead.

## Attenuverter offset
Some owners report that turning a CV attenuverter with nothing patched adds a small offset. This release does not change
calibration.

## Version information
The module reports **31.2C3**. The firmware-card image header still reads 31.2 (cosmetic).

## Release candidate
Tested on one module; see the [release notes](RELEASE-NOTES.md) for what is still open from 31.2C1 (long soak, card RESTORE).
