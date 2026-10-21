# Fixed bugs — 251e 30.7C1 (relative to Buchla 30.7)

None of these fixes has been run on hardware yet; see the [release notes](RELEASE-NOTES.md#test-status).

## 1. Stage knobs skip steps when turned fast; above about 200 steps per second they do nothing
**Symptom.** Turning a stage/value knob briskly skipped steps. Beyond roughly 200 steps per second (a quick flick) the knob had
no effect until you paused; with slightly dirty contacts the limit was lower (about 125–170 steps per second).
**Cause.** After each knob movement the module ignored all knob movement for about 5 ms, and every tiny contact flutter during a
spin restarted that 5 ms wait, so a steady fast turn never got through.
**Fix.** Each knob is now read as a pair of signals the moment it moves, and each step is counted once, however fast the knob
turns. Contact flutter between neighbouring positions cancels itself. At normal speed the knob behaves as before.

## 2. Turning two knobs together lost steps
**Symptom.** With two stage knobs turning at once, a noticeable share of the steps (a seventh at slow speed, about half at a brisk
turn) did not register.
**Cause.** All six knobs shared one wait period and one reader, so a movement on one knob swallowed or hijacked another's.
**Fix.** The knobs no longer share anything.

## 3. A step counted in the wrong direction on worn contacts
**Symptom.** On a knob with worn or noisy contacts, an occasional step went the wrong way (one wrong step costs two counts).
**Cause.** The direction was taken from where the contacts happened to rest after the movement, and a long contact flutter could
be mistaken for the resting position.
**Fix.** Direction is now taken from the order in which the two contacts change, and flutter that goes forth and back cancels
itself.

## 4. First click after power-up could be missed
**Symptom.** A knob left in one particular position at power-up ignored its first click.
**Cause.** The module did not note the starting position of each knob at power-up.
**Fix.** The starting position of every knob is read at power-up.

## 5. Panel redrew the wrong stage after an external RECALL or RESTORE
**Symptom.** After a preset was recalled or restored over the bus while the panel was in stage-edit mode, the displays showed
stage 1 of the new preset (and the stage number did not update) instead of the stage being edited. Re-selecting the stage fixed it.
**Cause.** The redraw looked up the stage number in a field that is never set.
**Fix.** The redraw uses the real stage being edited.

## 6. Bus SAVE / RECALL accepted any slot number
**Symptom.** A SAVE or RECALL over the bus with a slot number of 30 or more (there are only 30 slots, 0–29) was carried out
anyway; a RECALL of a high slot number could read beyond the preset area.
**Fix.** SAVE and RECALL for slot 30 or above are now ignored. Slots 0–29 work as before.

## 7. One byte of the "parameter edited" message was never set
**Symptom.** The short message the module sends on the bus after a panel parameter changes carried a leftover value in its last byte.
**Fix.** That byte now carries the module's own bus address.

## 8. Button contact bounce was sampled too quickly
**Symptom.** Button contacts that bounced for more than a millisecond or two could register as an extra press or release.
**Cause.** The debounce checked the buttons every 1.2 ms.
**Fix.** The debounce now samples about every 4 ms. Button response time is essentially unchanged.

## 9. A sequence with every stage set to zero interval froze the module
**Symptom.** If all 50 stages of a sequence were set to "zero interval" (skip), the module locked up, sound and panel, until power-cycled.
**Cause.** The code that skips zero-interval stages looked for a playable stage without any limit.
**Fix.** It now gives up after one pass through the stages.

## Version
The module reports **30.7C1** in the version announcement it sends from the panel.
