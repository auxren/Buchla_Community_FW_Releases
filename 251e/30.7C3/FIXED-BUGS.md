# Fixed bugs — 251e 30.7C3 (relative to Buchla 30.7)

30.7C3 is made of eleven sequencer and panel change sets on top of Buchla's 30.7, plus the calibration code described at the end. Items 1–9 are the first two sets and are unchanged from
[30.7C2](../30.7C2/FIXED-BUGS.md) (the knob fixes and the small bus and panel fixes). Items 10–18 are the nine new sequencer
sets. Only part of this has run on a real module; see the [test status](RELEASE-NOTES.md#test-status). After the fixes comes a section on the calibration code this image also carries; that is
an addition, not a bug fix.

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

## 10. Two sequencers at different tempos drifted apart; sync-next pulsed twice
**Symptom.** With one sequencer at 120 BPM and another at 240 BPM (both 1/16 notes), the faster one slipped against the slower one,
about 16 ms per 120-BPM bar. A sync-next stage that started another sequencer produced a double pulse at the sync point.
**Cause.** The length of a stage was rounded to a whole number of 0.25 ms ticks (240 BPM at 1/16 came out as 252 ticks instead of
250), and the rounding error was thrown away at every stage.
**Fix.** The unrounded length is kept and each sequencer carries its own remainder from stage to stage. In the model the 120/240
pair no longer drifts and the other pairs tried stay within one tick; the double pulse at a sync-next point is gone. Sync-next is
de-doubled only; it is not aligned to the tick (see [KNOWN-ISSUES.md](KNOWN-ISSUES.md)).

## 11. Tempo ran about 0.7 % faster than the tempo number
**Symptom.** At a tempo setting of 120 BPM a 1/16 stage lasted 124.1 ms instead of 125.0 ms.
**Fix.** The tempo constant is corrected, so a 1/16 stage at 120 BPM averages 125.00 ms (stage lengths alternate between 503 and 504
ticks). Relative tempos between sequencers are unchanged. This figure comes from the firmware model; it has not been measured on a
module (see [KNOWN-ISSUES.md](KNOWN-ISSUES.md)).

## 12. Pressing the pulse-select button while a sequence plays disturbed the timing
**Symptom.** Changing a stage's pulse width during playback made the running sequencer recompute its stage length from the edited
stage: a step could come early or late, or the sounding pulse could be cut or stretched (about 2.2 ms late in the worst case).
**Fix.** The button only stores the new width, lights the LEDs and sends the bus message. The new width applies the next time that
stage is entered.

## 13. The "trans" pulse was too short and unreliable for a 292e low pass gate
**Symptom.** The "trans" pulse lasted 3 ticks (0.74 ms); under main-loop load some pulses came out short or too weak to strike a 292e
in strike mode.
**Fix.** The pulse lasts 12 ticks (about 2.98 ms: 0.5 ms at full level, then half level). Its start is unchanged and the other pulse
widths are unchanged.

## 14. A pulse edge could be lost or stick
**Symptom.** Rarely, a pulse end written while the main loop was sending the output values was lost; the pulse stayed high (or a
pulse was missing) until the next CV step.
**Cause.** The main loop read the values, sent them, and only then cleared the "changed" mark, so a write made during the send
was forgotten.
**Fix.** The mark is cleared before the send, so such a write goes out on the next pass. A smaller race inside the send itself (three
instructions per channel) remains.

## 15. Nested loops jumped almost at random; sequencer 2 differed from sequencer 1
**Symptom.** An END jumped to the nearest available loop-begin, so loops did not nest; a begin's count behaved as a quota; playing in
reverse fell to stage 50; loop counters were never reset, so a stale count from an earlier run could skip a loop.
**Fix.** Loop brackets nest (the test pattern with begins on stages 2 and 4 plays `1 2 3 4 5 4 5 6 7 2 3 4 5 4 5 6 7 8`), each END
has its own counter, there is no wrap to stage 50, and START zeroes the sequencer's loop counters.

## 16. A "ghost loop" remained after switching loop-begin off
**Symptom.** Pressing loop-begin twice on a stage left its count at A, so the stage silently looped back for ever.
**Fix.** Clearing loop-begin also sets the count to 0. Clearing it on a stage that had its own count before begin was set also
clears that count.

## 17. CV stage select flickered at stage boundaries
**Symptom.** With the stage chosen by an external CV parked at an edge between two stages, a little noise made the stage flicker; in
direct mode every flip re-entered the stage (CV output stepped, pulse re-armed).
**Fix.** A new stage is accepted only when the code is at least one code inside it (a two-code band at each boundary). A clean
0–255–0 ramp changes the stage exactly 49 times up and 49 times down. A CV parked exactly on the first code of a stage keeps the
previous stage. The table itself, the 50 stages and both modes are unchanged.

## 18. SAVE stopped every sequencer for about 40 ms and left them permanently late
**Symptom.** Saving a preset stopped all four sequencers for about 40 ms (about 48 ms for slots 9, 18 and 27), and the sequence
stayed that much late, accumulating with each SAVE.
**Fix.** SAVE no longer gates the sequencers; ticks lost while the processor waits for flash are made up afterwards, and the output
values are sent after each flash command. Expected result: an edge that falls inside a flash command is at most 4 ms late, then the
sequence is back on its grid with no accumulated offset. This relies on the processor's cycle counter running during a flash wait,
which has not been measured; if it does not, the behaviour falls back to that of 30.7C2.

## What the calibration code adds (not a bug fix)
This image also contains code that lets a Xenomorpher measure, and optionally store, a calibration for the module's four CV outputs.
It adds these commands on the 200e bus, none of which Buchla's firmware knows: 0x10 (hold one CV output at a chosen value), 0x11
(release all held outputs), 0x12 (stage bytes of a record), 0x0B (commit the staged record) and 0x18 (read the stored record or the
status). Holding an output is released by itself 5 seconds after the last hold command.

- The module can keep **one** user calibration record, in flash page 0x8007FE00. If a valid record is present the module applies it
  to the four CV outputs.
- A module with no stored record behaves like the plain sequencer-only build (items 1–18, nothing else changed).
- A record is written only by a deliberate action from a Xenomorpher: the commit command is accepted only for a complete, correctly
  checksummed record made for this module type; a damaged or interrupted write is ignored and the module runs as if it had no record.
  **No public tool writes a record yet.** Nothing in normal use sends these commands.
- The module pauses for a few milliseconds while a record is being saved.
- To load the calibration code the update programs one more 512-byte flash page (0x80015E00) than Buchla's own update does. This
  space is unused in Buchla's image.

See [KNOWN-ISSUES.md](KNOWN-ISSUES.md) for what has and has not been proven about this code.

## Version
The module reports **30.7C3** in the version announcement it sends from the panel. See
[KNOWN-ISSUES.md](KNOWN-ISSUES.md#two-different-builds-report-307c3) for how to tell this image from an earlier internal build with the same string.
