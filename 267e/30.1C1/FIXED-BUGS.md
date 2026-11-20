# Fixed bugs: 267e 30.1C1 (relative to Buchla 30.1)

## 1. The external c.v. <-> random mix pot was not recalled with a preset
**Symptom.** Each random section (A and B) has a pot that mixes an external control voltage with the random voltage. A preset
stored its position, but recalling the preset did not move the mix: it kept following wherever the pot physically was.
**Fix.** The mix now comes from the preset, like the module's other pots. It follows the recalled preset at power-up and on
recall, and picks up a turn of the pot once you move it.

**What you will notice.**
- A recalled preset sets the mix. The pot's physical position then no longer matches it until you turn the pot.
- Turning the pot is picked up after a small movement (its third change within a second) and the stored value then moves toward
  the pot proportionally, as on the module's other pots. Before, the mix followed the pot directly.
- At power-up the mix comes from the first preset, not from the panel. After a fresh install the presets are empty, so both
  sections start fully on the external control voltage until you turn the pots.

## 2. A damaged preset could push the mix out of range
**Fix.** The stored mix value is limited to its valid range when it is read, so a damaged or foreign preset record cannot drive
the mix outside the range between external c.v. and random. A wrapped out-of-range value is not clamped to the end; it simply
cannot exceed the valid range.
