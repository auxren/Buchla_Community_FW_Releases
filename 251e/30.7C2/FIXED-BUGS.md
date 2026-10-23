# Fixed bugs — 251e 30.7C2 (relative to Buchla 30.7)

Items 1–4 are the knob fixes; 30.7C1's version of them regressed on a worn knob and is replaced here (see the
[release notes](RELEASE-NOTES.md#what-changed-since-307c1)). Items 5–9 are unchanged from 30.7C1. None of this has been run on
hardware in this form; see the [test status](RELEASE-NOTES.md#test-status).

## 1. Stage knobs skip steps when turned fast; above about 200 steps per second they do nothing
**Symptom.** Turning a stage/value knob briskly skipped steps. Beyond roughly 200 steps per second (a quick flick) the knob had
no effect until you paused; with slightly dirty contacts the limit was lower (about 125–170 steps per second).
**Cause.** After each knob movement the module ignored all knob movement for about 5 ms, and every tiny contact flutter during a
spin restarted that 5 ms wait, so a steady fast turn never got through.
**Fix.** The 5 ms blackout is gone. A knob movement starts a short settling check (about 2 ms) for that knob only, after which
the step is counted once. A fast flick is limited only by that settling time: about 250 steps per second on clean contacts,
100–150 per second on worn ones (close to Buchla's 30.7 on a single knob, but without the blackout that flutter kept restarting).
At normal speed the knob behaves as before.

## 2. Turning two knobs together lost steps
**Symptom.** With two stage knobs turning at once, a noticeable share of the steps (a seventh at slow speed, about half at a brisk
turn) did not register.
**Cause.** All six knobs shared one wait period and one reader, so a movement on one knob swallowed or hijacked another's.
**Fix.** Each knob has its own settling check and its own memory of where it was. The knobs no longer share anything.

## 3. A step counted in the wrong direction on worn contacts
**Symptom.** On a knob with worn or noisy contacts, an occasional step went the wrong way (one wrong step costs two counts). On
30.7C1 this became much worse on such a knob: bursts of steps in random directions, which drove the CV-out value to 0.
**Cause.** Direction has to be read from where the two contacts rest after a click. 30.7 could mistake a long contact flutter for
the resting position; 30.7C1 read the contacts the instant the first one moved, before the second one had settled.
**Fix.** Direction is taken only after both contacts have held still for about 2 ms, and a movement that flutters back to where
it started counts nothing. Flutter longer than the settling time can still be misread, as on Buchla's 30.7.

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
**Fix.** That byte now carries the module's own bus address. (The preset manager does not read that byte, so this changes nothing
visible; the message itself is what makes a preset manager show the preset as edited, which is by design.)

## 8. Button contact bounce was sampled too quickly
**Symptom.** Button contacts that bounced for more than a millisecond or two could register as an extra press or release.
**Cause.** The debounce checked the buttons every 1.2 ms.
**Fix.** The debounce now samples about every 4 ms. Button response time is essentially unchanged.

## 9. A sequence with every stage set to zero interval froze the module
**Symptom.** If all 50 stages of a sequence were set to "zero interval" (skip), the module locked up, sound and panel, until power-cycled.
**Cause.** The code that skips zero-interval stages looked for a playable stage without any limit.
**Fix.** It now gives up after one pass through the stages.

## Version
The module reports **30.7C2** in the version announcement it sends from the panel.
