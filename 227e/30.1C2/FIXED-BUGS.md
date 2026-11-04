# Changes — 227e 30.1C2 (relative to 30.1C1)

30.1C2 keeps 30.1C1's button fix ([30.1C1 FIXED-BUGS](../30.1C1/FIXED-BUGS.md)) and adds one new feature and two bug fixes.
The checks behind them were run on an emulator of the firmware unless the [test status](RELEASE-NOTES.md#test-status) says a module showed it.

## 1. Pan mode (new feature)
**What.** Hold a swirl button for about 0.8 s: that input leaves swirl and becomes a pan input. The swirl LED blinks about twice a second while it is in pan mode.
- **Rate input** = position along C > A > B > D: 0 V = about 100 % C, 3.33 V = about 100 % A, 6.67 V = about 100 % B, 10 V = about 100 % D; between two neighbours the
  mix is linear, so each side is about -6 dB at the midpoint (a linear crossfade, not equal-power).
- **Ampl input** = slew limiter on the rate input. The time a full 0-10 V move takes goes from instant to about 17 s.
- **Rate knob and ampl knob** are attenuators of their inputs. Knob fully counter-clockwise: the input adds nothing. Rate knob fully
  counter-clockwise, or nothing patched into the rate input, leaves the position at 100 % C. The top of the knob range counts as fully clockwise.
- **Hold again** to leave pan mode (LED off). The input then runs the standard mode, not swirl.
- **Presets** keep the pan state (store, recall, backup, restore; at power-up if slot 0 holds it). Presets made by earlier firmware are read as before.
- The position is updated about 93 times a second (once per panel look), so it suits control voltages, not audio-rate signals.

**Because of the hold, a short press of a swirl button now acts when released** (previously when pressed). Holds of other buttons are unchanged.

## 2. RESTORE wrote a stale slot when a card read failed
**Symptom.** If the module's card read failed during a RESTORE, the module wrote whatever was left in its buffer into the bank (for example the
previous slot's data landed in slot 0).
**Fix.** The module tries each read up to 4 times; if it still fails, the RESTORE stops without writing that slot or any later one. The completion reply is still
sent, so the host sees a normal finish: read the bank back after a restore.

## 3. Block-move (0x07) and exchange (0x08) commands accepted slots that do not exist
**Symptom.** With out-of-range slot numbers the move could loop forever or write past slot 29.
**Fix.** Both commands refuse out-of-range slots and write nothing. In-range moves behave as before (overlapping moves with the destination above the first slot still cascade, as in Buchla's 30.1).

## Version
The module reports **30.1C2** in its version announcement.
