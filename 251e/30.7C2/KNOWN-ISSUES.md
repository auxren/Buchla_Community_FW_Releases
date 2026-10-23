# Known issues and behaviour that is unchanged from Buchla's 30.7

## Not yet run on hardware
This candidate has been checked in the lab only. Its predecessor 30.7C1 ran on one module and showed a knob regression that
this build is meant to fix; the fix itself has not been on a module. The [release notes](RELEASE-NOTES.md#test-status) say what
to check first.

## One knob step per click is assumed
The knob handling counts every click of a knob as one step, as Buchla's 30.7 implies at slow speed. If a knob on your unit steps
two stages per click, please go back to Buchla's 30.7 and report it.

## Very fast turns
Each knob needs its contacts to hold still for about 2 ms before a step is counted. A flick faster than roughly 250 steps per
second on clean contacts, or 100–150 per second on worn ones, loses steps (Buchla's 30.7 stopped counting altogether above
about 200 per second). Contact flutter that lasts longer than the 2 ms settling time can still be read as a step in the wrong
direction, as on 30.7. These are limits of the knob, not of the sequencer.

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
The module reports **30.7C2**. The firmware-card image header still reads 30.7 (cosmetic).

## Release candidate
This is release candidate 2. It replaces 30.7C1, which should no longer be flashed.
