# 259e Twisted Waveform Generator — Community firmware 31.2C3 (release candidate 3)

**Based on:** Buchla 259E firmware **31.2** (`259E_312.hex`, 11/26/2024, sha256
`556a839b2b0216bbf4e23ba596b0b7a92c202e702438018cf7c39adf5b20c096`), via community
[31.2C1](../31.2C1/RELEASE-NOTES.md) and [31.2C2](../31.2C2/RELEASE-NOTES.md). Everything not listed under
[Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 31.2. The version this build reports (the panel's version
announcement on the bus) is **31.2C3**.

**Status: release candidate.** The 31.2C1 fixes and the 31.2C2 Original-table mode were flashed and checked on one 259e.
**The new part of 31.2C3, remembering the choice, has not yet run on hardware.** See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `259Ev312_31.2C3.hex` | firmware image (Intel HEX) | `16b29e07a642e6895106f1034c8c4571895e38b65aef27e6e46177b439adfaad` |
| `259Ev312_31.2C3.card.bin` | the same image as a 64 KB USB-Firmware-Card image | `c3aa3579aa2110d96c58fb881377b112621790183b08c0dfcd454e54164c5f4b` |

The file names keep Buchla's `259Ev312…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 31.2; that is cosmetic. The module itself reports 31.2C3.

The image occupies exactly the same flash areas as Buchla's own 31.2 update. The waveshaping tables stored elsewhere in the
module, the calibration area and the preset bank are not touched by the update.

## What changed (summary)
31.2C3 makes the Original-table choice of 31.2C2 stick (details in [FIXED-BUGS.md](FIXED-BUGS.md)):

**The choice is remembered.** Power up holding **TIMBRE** for the Original tables, or holding **SHAPE** for Twisted; from then
on every normal power-up comes back in the mode you last chose. The module keeps it in one byte of its own calibration area,
written in a way that never blanks that area, so a power loss during the write cannot cost you your presets. Up to about a
thousand changes fit; after that the last choice stays.

From 31.2C2, unchanged: **Original wavetables.** The 259e carries fourteen factory transfer tables in its flash; the Twisted
firmware uses eight of them (timbres 1 to 4 on each side) and turns the a, b and c positions into memory scans. In Original
mode a, b and c point at the six factory tables the Twisted firmware does not use, the ones from the original 259e; the FM
knobs act as FM for a, b and c, as they did on the original, and the memory-scan indication stays off. Timbres 1 to 5,
presets, the preset format, the bus protocol, card BACKUP/RESTORE and knob feel are unchanged.

## Test status
From 31.2C1, done on hardware (one 259e on a live 200e bus): flash, boot, QUERY, preset BACKUP, version frame, panel taps,
knobs and sound. **Pass.** From 31.2C2, done on the same module on 2026-10-20: power-up with TIMBRE held brings up the
Original tables. **Pass.**

**Not yet run on hardware:** remembering the choice across power cycles (31.2C3). Checked in the lab only: every power-up
case was replayed in an emulator against the firmware's own flash byte writer. Owners who try it: please report whether the
mode survives a normal power cycle after a TIMBRE hold, and whether a SHAPE hold brings Twisted back and that survives too.

Also still open from 31.2C1: the exact freeze scenario of fix 1, card RESTORE, SAVE / RECALL across a power cycle, long soak.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 31.2 the same way.
