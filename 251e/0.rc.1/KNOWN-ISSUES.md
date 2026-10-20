# Known issues and behaviour that is unchanged from Buchla's 30.7

## Not yet run on hardware
This candidate has been checked in the lab only and has never run on a module. Items listed under "Not yet run on hardware" in
the [release notes](RELEASE-NOTES.md) are still to be completed.

## One knob step per click is assumed
The new knob handling counts every step of a knob once. It assumes a click of a knob is one step, as Buchla's 30.7 implies at slow
speed. If a knob on your unit steps two stages per click, please go back to Buchla's 30.7 and report it.

## Very fast turns with worn contacts
Knob steps are counted correctly at any speed on clean contacts. If a knob's contacts bounce for about 2 ms or more, steps are
counted correctly up to roughly 250 steps per second; above that the bounce itself can add or subtract steps. This is the physical
limit of the knob, not of the firmware.

## Remote Enable tap saves to preset 0
With no preset manager polling, tapping Remote Enable saves the current settings to preset slot 0 (documented in Buchla's 200e
guide). This is unchanged. All 30 presets live in one flash area, so a power loss during a SAVE can corrupt presets or make the
module reformat its bank. Keep a BACKUP of your presets.

## BACKUP while in Remote Enable
Buchla's note stands: take the 251e out of Remote Enable before a card BACKUP. With Remote Enable on, a BACKUP writes the module's
whole preset bank (about 63 KB) to the card from the starting address the manager supplies, which can overwrite other modules'
areas. Unchanged.

## Buttons share one debounce
All 21 buttons share one debounce state. Pressing a second button while the first is held can lose the first button's release
(modifier "held" states can stick; a Remote Enable hold may not be cancelled). Unchanged; only the sampling rate was changed.

## Waits on the bus
Several bus transfers still wait for the bus with no time limit, and the hardware watchdog remains off, as in 30.7. A stuck bus can
freeze the panel until power-cycle. Long operations (SAVE, BACKUP, RESTORE) can also drop panel events while they run.

## Version information
The module reports **0.rc.1**. The firmware-card image header still reads 30.7 (cosmetic).

## Release candidate
This is release candidate 1.
