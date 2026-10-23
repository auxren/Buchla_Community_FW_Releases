# 251e Quad Sequential Voltage Source — Community firmware 30.7C2 (release candidate 2)

**Based on:** Buchla 251E firmware **30.7** (`251Ev307.hex`, Buchla download dated 2019-06-04, sha256
`68e7261af629b332f77c3eaad8ed06c86af1ed7a48d1d5be6a545800b3a7dab2`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 30.7. The version this build reports
(the panel's version announcement on the bus) is **30.7C2**; the number is Buchla's version followed by `C` (a community build
made with Claude) and a revision number, so the module always says what it is based on.

**Status: release candidate 2, not yet run on hardware.** It replaces [30.7C1](../30.7C1/RELEASE-NOTES.md), whose first
run on a module (2026-10-22) showed a regression on a worn knob; see [What changed since 30.7C1](#what-changed-since-307c1).

## Files
| file | what | sha256 |
|---|---|---|
| `251Ev307_30.7C2.hex` | firmware image (Intel HEX) | `46d827b581bc36d3bd9239153c823e5d945c6f77f25911d973b9e5d8f34b32a9` |
| `251Ev307_30.7C2.card.bin` | the same image as a 224 KB firmware-card image (the larger card layout used by the 200e's 32-bit modules) | `7e54f43883fe24e3bbad6a2f38095281bc14ec116d9f18a5a92a1ed14da4f6f2` |

The file names keep Buchla's `251Ev307…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 30.7; that is cosmetic. The module itself reports 30.7C2.

The image occupies exactly the same flash areas as Buchla's own 30.7 update. The preset bank is not touched by the update.

## What changed since 30.7C1
On the first module to run 30.7C1 the tempo, init delay, interval and stage knobs were better than on Buchla's 30.7 but still
jumped forward now and then, and the CV-out knob got worse: its value kept snapping back to 0 and could not be raised past 2.0 V.

The cause was 30.7C1's new knob reading. It decided a knob's direction the instant the knob's first contact moved, and on a knob
whose second contact is noisy at that moment (a worn or dirty knob) it counted a burst of steps in random directions. Fast
bursts count 0.4 V per step, so the CV value ran into its lower limit. Buchla's 30.7 waited about 2 ms for both contacts to
settle before deciding, which hid that noise.

30.7C2 waits for the contacts to settle again, as Buchla's 30.7 did, but does it for each knob separately and without the
5 ms blackout that caused 30.7's skipped steps. On a noisy knob every click now counts exactly once, in the right direction.
The trade-off: a very fast flick is limited to roughly 250 steps per second on clean contacts and about 100–150 per second
with worn contacts, which is about where Buchla's 30.7 was, instead of the "any speed" of 30.7C1. Turning two knobs at once still
loses nothing. Details in [FIXED-BUGS.md](FIXED-BUGS.md) item 1 and [KNOWN-ISSUES.md](KNOWN-ISSUES.md).

Nothing else differs from 30.7C1.

## What changed relative to Buchla 30.7 (summary)
Nine problems in 30.7 are fixed. Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. Turning a stage knob briskly skipped steps, and above roughly 200 steps per second the knob did nothing at all.
2. Turning two or more knobs together lost steps even at moderate speed.
3. With worn knob contacts a step could be counted in the wrong direction (30.7C1 made this worse; 30.7C2 fixes it).
4. The first click of a knob after power-up could be missed.
5. The panel did not redraw the right stage after a preset was recalled or restored over the bus.
6. Preset SAVE / RECALL commands over the bus with an out-of-range slot number were acted upon.
7. One byte of the "parameter edited" message the module sends on the bus was never filled in.
8. Button contact bounce was sampled very quickly; sampling is now slower and more tolerant.
9. A sequence with every stage set to zero interval froze the module.

Sound, CV outputs, sequencing, presets, the preset format, the bus protocol and card BACKUP/RESTORE are unchanged.

## Test status
**Not yet run on hardware.** 30.7C1 was run on one module, which confirmed items 1, 2 and 4 improve knob behaviour and found the
regression described above; 30.7C2's knob reading has only been checked in the lab, against a model of clean, bouncy and worn
knob contacts. Please test, in this order, and report:
1. On a knob that misbehaved on 30.7C1 (typically CV-out): 40 slow clicks up from 0.0 must read 4.0 with no backward step; 20 fast
   clicks from 0.0 should read about 8.0 and never fall; 40 clicks back must return to 0.0.
2. Every knob: 40 steps forward and 40 back, slow and brisk, must return to the starting value.
3. Two knobs turned together, a quick flick, a knob resting between clicks while the panel is tapped (no spontaneous steps).

One assumption still needs a real unit to settle: the knob handling counts each click of a knob as one step, which is what
Buchla's 30.7 does at slow speed. If on your unit a knob moves **two** stages per click, go back to Buchla's 30.7 and please
report it. See [KNOWN-ISSUES.md](KNOWN-ISSUES.md).

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 30.7 the same way.
