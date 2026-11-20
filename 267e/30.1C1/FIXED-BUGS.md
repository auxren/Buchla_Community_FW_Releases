# Fixed bugs: 267e 30.1C1 (relative to Buchla 30.1)

## 1. The external c.v. <-> random mix pot was not recalled with a preset
**Symptom.** Each random section (A and B) has a pot that mixes an external control voltage with the random voltage. A preset
stored its position, but recalling the preset did not move the mix: it kept following wherever the pot physically was.
**Fix.** The mix now comes from the preset, like the module's other pots. It follows the recalled preset at power-up and on
recall, and picks up a turn of the pot once you move it.

## 2. A damaged preset could push the mix out of range
**Fix.** The stored mix value is limited to its valid range when it is read, so a damaged or foreign preset record cannot drive
the mix outside the range between external c.v. and random. A wrapped out-of-range value is not clamped to the end; it simply
cannot exceed the valid range.
