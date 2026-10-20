# 251e Quad Sequential Voltage Source — Community firmware 0.rc.1 (release candidate 1)

**Based on:** Buchla 251E firmware **30.7** (`251Ev307.hex`, Buchla download dated 2019-06-04, sha256
`68e7261af629b332f77c3eaad8ed06c86af1ed7a48d1d5be6a545800b3a7dab2`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 30.7. The version this build reports
(the panel's version announcement on the bus) is **0.rc.1**; this is the community numbering track, as for the 259e and 272e.

**Status: release candidate, not yet run on hardware.** See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `251Ev307_0.rc.1.hex` | firmware image (Intel HEX) | `6a525398977b66dac93d6482971525bc15ed3003f0176606a4f085fa865f221a` |
| `251Ev307_0.rc.1.card.bin` | the same image as a 224 KB firmware-card image (the larger card layout used by the 200e's 32-bit modules) | `b570df8c0b3d0bf15ac679d512428292b8ecd2c2fc85f31362c75c65a34fd457` |

The file names keep Buchla's `251Ev307…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 30.7; that is cosmetic. The module itself reports 0.rc.1.

The image occupies exactly the same flash areas as Buchla's own 30.7 update. The preset bank is not touched by the update.

## What changed (summary)
Nine problems in 30.7 are fixed. Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. Turning a stage knob briskly skipped steps, and above roughly 200 steps per second the knob did nothing at all.
2. Turning two or more knobs together lost steps even at moderate speed.
3. With worn knob contacts a step could be counted in the wrong direction.
4. The first click of a knob after power-up could be missed.
5. The panel did not redraw the right stage after a preset was recalled or restored over the bus.
6. Preset SAVE / RECALL commands over the bus with an out-of-range slot number were acted upon.
7. One byte of the "parameter edited" message the module sends on the bus was never filled in.
8. Button contact bounce was sampled very quickly; sampling is now slower and more tolerant.
9. A sequence with every stage set to zero interval froze the module.

Sound, CV outputs, sequencing, presets, the preset format, the bus protocol and card BACKUP/RESTORE are unchanged.

## Test status
**Not yet run on hardware. Checked in the lab only.** No module has been flashed with this image. In particular, none of the
following has been tried on a real 251e: the knob changes (items 1–4), the panel redraw after RECALL, the bus slot check, the
zero-interval case, or a long soak. Reports are welcome.

One assumption needs a real unit to settle: the new knob handling counts each step of a knob once, assuming each click of a
knob produces one step in Buchla's firmware (which is what Buchla's own 30.7 does at slow speed). If on your unit a knob moves
**two** stages per click, go back to Buchla's 30.7 and please report it. See [KNOWN-ISSUES.md](KNOWN-ISSUES.md).

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 30.7 the same way.
