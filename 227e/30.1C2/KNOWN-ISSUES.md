# Known issues and behaviour that is unchanged from Buchla's 30.1

## Test status
This is a pre-release. It was loaded on one module on 2026-11-04 and the owner saw the version, pan mode, and the pan state surviving a preset
store and recall. Everything in [RELEASE-NOTES.md](RELEASE-NOTES.md#test-status) under "Not checked" is untested on hardware. The pan, RESTORE and block-move code
was otherwise checked in an emulator of the firmware.

## Going back to 30.1 or 30.1C1 with pan presets
A preset that stores pan mode, given to Buchla's 30.1 or to 30.1C1, plays as swirl, and its swirl button cannot switch it off until a preset without pan is recalled. Before going back, take every input out of pan mode and re-store the presets you want to keep, or avoid storing pan in them. This is expected from the code; it has not been tried on a module.

## No manual pan in pan mode
Both knobs are attenuators of their inputs, so with the rate knob fully counter-clockwise, or nothing patched into the rate input,
the position is pinned at 100 % C. To place a signal you must patch a control voltage into the rate input.

## One swirl button at a time
If two swirl buttons are pressed together, only one can enter pan mode; a second button pressed while the first is being held acts as a normal press.
Two buttons changing in the same few milliseconds already overwrote each other in Buchla's 30.1 and still do.

## Linear crossfade
The mix between neighbouring outputs is a linear crossfade, about -6 dB on each side at the midpoints, not an equal-power one. Expect a level dip between positions.

## Position updates are stepped
The position is recalculated about 93 times a second (about 61 per second if the clock were 16 MHz). This is fine for control voltages and slow modulation, not for audio-rate signals.

## The blink restarts together
The blink phase is shared: putting one input into pan mode restarts the blink for all inputs that are in pan mode.

## An aborted RESTORE is silent to the host
If a RESTORE stops after four failed reads, the module still sends its normal completion reply. Always read the bank back after a restore.

## Overlapping block moves still cascade
The new range check only refuses slot numbers that do not exist. A block move whose destination overlaps the source above it still repeats data, as in Buchla's 30.1.

## Extra flash pages
The update programs two pages (`0x3400` and `0x3600`) that Buchla's own update never writes. See [INSTALL.md](INSTALL.md#the-extra-flash-pages). They sit inside the area the loader erases, but the USB-card route has not been tried.

## Listening check for clicks
The blink makes the module refresh its panel shift registers about every 257 ms while any input is in pan mode. A listening check for a tick about every quarter second (about 4 Hz) found none so far; it has not been measured on a scope. Please report a tick if you hear one.

## Unproven timing and switch bounce
- The 0.8 s hold time and the blink rate are calculated from the module's processor clock (24.5 MHz, decoded from the firmware, accurate to about 2 %); they have not been timed on a module. The 17 s maximum glide and the 93 updates a second scale with the same clock figure. If the clock were 16 MHz the hold would be about 1.2 s and the blink about 1.3 Hz, the maximum glide about 26 s and the updates about 61 per second.
- The input scaling (0 to 10 V being the full range of the input) and which jack is which output are assumed from standard-mode behaviour and not metered.
- Switch bounce against the 30.1C1 button qualifier (two looks in a row, about 21 ms for a certain press, from about 11 ms for a possible one) has not been measured. A button that double-triggers is worth reporting.

## Unchanged from Buchla's 30.1
- Blips shorter than about 11 ms are ignored (the panel looks at the buttons every 10.7 ms).
- Some bus transfers wait with no time limit; a fault on the bus can still hang the module until a power cycle.

## Version information
The module reports **30.1C2**. The firmware-card image header still reads 30.1 (cosmetic).
