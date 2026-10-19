# Known issues and behaviour that is unchanged from Buchla's 31.2

## Knobs stop a little short of full scale when swept upwards
Buchla's 31.2 keeps a small dead band on each knob so that noise and direction reversals do not jitter the parameter. A side
effect is that a knob swept upwards reads about 0.7 % below its true position, so the very top of a parameter's range cannot
be reached from below (sweeping down reaches the bottom exactly). This is unchanged in 0.rc.1 because changing it changes
the knob feel; it is a candidate for a later release.

## All 30 presets live in one flash block
Every SAVE (from the panel, over the bus, or a card RESTORE) rewrites the entire preset bank. A power loss during the save
window loses all 30 presets, after which the module starts with a default bank. This is Buchla's original design and is
unchanged. Keep a BACKUP of your bank.

## Card BACKUP / RESTORE waits
The card transfer routines still wait for the bus with no time limit, with the audio engine paused for the duration of the
transfer, as in 31.2. A wedged card during a transfer can still freeze the module. The hardware watchdog remains disabled,
as in 31.2.

## Remote LED turns on by itself
After power-up or a preset recall, the first knob or button edit turns Remote Enable on if no preset manager has started
polling. This is Buchla's original behaviour and is unchanged.

## Holding Remote saves to preset 0
Holding the Remote button for about 0.4 s (when no preset manager is polling) saves the current settings into preset slot 0
and re-initialises the bus interface. This is Buchla's original behaviour, as documented for the 200e, and is unchanged.
When a preset manager is polling, the same hold sends the version announcement instead.

## Attenuverter offset
Some owners report that turning a CV attenuverter (for example Morph) with nothing patched adds a small offset. The
attenuverter multiplies the input against the module's stored CV calibration; a stale calibration leaves a residual term.
This release does not change calibration.

## Version information
The module reports **0.rc.1**. The firmware-card image header still reads 31.2 (cosmetic).

## Release candidate
Items listed under "Not yet run on hardware" in the [release notes](RELEASE-NOTES.md) are still to be completed; in
particular the freeze scenario of fix 1 has been reproduced only in the lab, not on a live bus.
