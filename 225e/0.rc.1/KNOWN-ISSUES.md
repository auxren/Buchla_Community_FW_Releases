# Known issues and behaviour that is unchanged from Buchla's 30.9

## Encoder chatter on a detent edge
The encoder still has no debounce of its own. Contact chatter exactly on a click boundary can produce pairs of opposite clicks and extra display redraws (visible as flicker). This fix removes the lost clicks, not the chatter. A change to this would alter when backward clicks register, so it is left for a later release after a feel check.

## Tap versus hold on one panel button
The threshold between a tap and a hold on one panel button is counted in passes of the module's main loop, not in time: about 0.2 s when idle, shifting with how busy the module is. A press held longer than that counts as a hold. Unchanged.

## The knob pauses during long operations
While a preset dump or restore over the bus, or a flash save, is in progress, encoder clicks are not processed and are lost. Unchanged.

## A silent bus device can stall the panel
If a device on the bus does not answer, the module can wait for it without a time limit. Unchanged.

## Panel button thresholds
The panel buttons are read through a resistor ladder whose converter timing may be tighter than the part's data sheet recommends. We suspect, but have not confirmed, that this causes an occasional missed or spurious press near a threshold. Unchanged.

## MIDI input during stalls
If the module stalls long enough for the MIDI input buffer to fill, the buffer is emptied and incoming MIDI bytes are lost. Unchanged.

## Power-up encoder position
If the encoder rests at its other detent position at power-up, the first click can be counted wrongly. Unchanged.

## Version information
The module reports **0.rc.1**. The firmware-card image header still reads 30.9 (cosmetic).

## Release candidate
This build has **not yet been run on a module**; it has only been checked in the lab. Everything above that is described as fixed is
unconfirmed on hardware until someone tries it.
