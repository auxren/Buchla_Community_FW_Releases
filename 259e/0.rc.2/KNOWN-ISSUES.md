# Known issues and behaviour that is unchanged from Buchla's 31.2

## The Original-table mode has not yet run on hardware
The power-up selection and the Original-table mode are new in 0.rc.2 and have been checked in the lab only. Things to
watch for and report: whether a, b and c in Original mode sound like tonal tables that fold with Warp; whether the WAVE hold
at power-up leaves the timbre and side where they were; what the timbre LEDs show for a, b and c in Original mode. If the
module misbehaves, powering up without WAVE gives the already-tested Twisted behaviour, and Buchla's 31.2 can be reflashed.

## The choice is not remembered
Original mode has to be selected at every power-up by holding WAVE. A stored choice is planned for a later release; it
needs a flash write that has not been tested yet.

## Order of the original tables
The three original tables per side are assigned to a, b and c in the order they sit in the module's memory. The original
259e may have numbered them differently. If you know the original order, say so and it can be changed.

## Knobs stop a little short of full scale when swept upwards
Buchla's 31.2 keeps a small dead band on each knob so that noise and direction reversals do not jitter the parameter. A side
effect is that a knob swept upwards reads about 0.7 % below its true position. Unchanged because changing it changes the
knob feel.

## All 30 presets live in one flash block
Every SAVE rewrites the entire preset bank. A power loss during the save window loses all 30 presets. Buchla's original
design, unchanged. Keep a BACKUP of your bank.

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
The module reports **0.rc.2**. The firmware-card image header still reads 31.2 (cosmetic).

## Release candidate
Items listed under "Not yet run on hardware" in the [release notes](RELEASE-NOTES.md) are still to be completed.
