# 251e Quad Sequential Voltage Source — Community firmware 30.7C3 (release candidate 3)

**Based on:** Buchla 251E firmware **30.7** (`251Ev307.hex`, Buchla download dated 2019-06-04, sha256
`68e7261af629b332f77c3eaad8ed06c86af1ed7a48d1d5be6a545800b3a7dab2`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 30.7. The version this build reports
(the panel's version announcement on the bus) is **30.7C3**; the number is Buchla's version followed by `C` (a community build)
and a revision number, so the module always says what it is based on.

**Status: pre-release (release candidate 3), only partly tested on hardware.** Of the 11 bench checks of the sequencer fixes, 2
passed on a real module and 9 have not been run. The calibration code in this image was loaded onto a real module and measured
against, but **no calibration record has ever been written to a real module with this firmware**. It follows
[30.7C2](../30.7C2/RELEASE-NOTES.md); see [Test status](#test-status). Not a stable release.

## Files
| file | what | sha256 |
|---|---|---|
| `251Ev307_30.7C3.hex` | firmware image (Intel HEX) | `d4ed6432953203e39b50b6bebafce3121ab90e56b258984cccbadda0226f31f9` |
| `251Ev307_30.7C3.card.bin` | the same image as a 224 KB firmware-card image (the larger card layout used by the 200e's 32-bit modules) | `ac34bb71121fd9173c42e08b8f7abc6e8949c07e522f1140b0cdfb3d521b3ebd` |

The file names keep Buchla's `251Ev307…` naming pattern because Buchla's flashing tools read the module and version from it.
The module itself reports 30.7C3.

**An earlier internal build without the calibration code reports the same `30.7C3`.** Tell them apart by the sha256 of the file you
load (above) and, on the bus, by the calibration status request, which only this image answers. See [KNOWN-ISSUES.md](KNOWN-ISSUES.md#two-different-builds-report-307c3).

Buchla's own update programs 112 flash pages; this image programs those 112 and one more page of previously unused space, which
holds the calibration code. The preset bank is not written by the update. See [INSTALL.md](INSTALL.md#the-extra-flash-page).

## What changed relative to 30.7C2
30.7C3 adds nine sequencer fixes to 30.7C2's nine fixes (the knob handling and the small bus and panel fixes, unchanged), and
carries the code for a Xenomorpher to calibrate the four CV outputs. Details in [FIXED-BUGS.md](FIXED-BUGS.md).

New sequencer fixes (items 10–18):
10. Two sequencers at different tempos (120 and 240 BPM) drifted apart, and sync-next produced a double pulse.
11. The tempo ran about 0.7 % faster than the tempo number (a 1/16 at 120 BPM lasted 124.1 ms instead of 125.0 ms).
12. Pressing pulse-select while a sequence played could make a step early or late, or cut the sounding pulse.
13. The "trans" pulse was only 0.74 ms and unreliable for a 292e low pass gate; it is now about 2.98 ms.
14. A pulse end could rarely be lost, leaving a pulse stuck high or missing.
15. Nested loops jumped almost at random, sequencer 2 differed from sequencer 1, and loop counters were never reset by START.
16. A "ghost loop" remained after switching loop-begin off.
17. CV stage select flickered at stage boundaries.
18. SAVE stopped every sequencer for about 40 ms and left them permanently late.

Calibration code (an addition, not a fix): bus commands 0x0B, 0x10, 0x11, 0x12 and 0x18 let a Xenomorpher hold a CV output at a
chosen value, measure it, and optionally store **one** user calibration record in flash page 0x8007FE00, which the module then applies
to its four CV outputs. A module with no stored record behaves like the plain sequencer-only build. A record can only be written by
a deliberate action from a Xenomorpher; **no public tool writes one yet**.

Sound, the preset format, the rest of the bus protocol and card BACKUP/RESTORE are unchanged. Known bugs in Buchla's 30.7 that this
build does **not** fix (among them a sync-next setting that freezes the module, and bus COPY/SWAP frames that can erase flash) are
listed in [KNOWN-ISSUES.md](KNOWN-ISSUES.md).

## Test status
**Partly tested.** What has run on a real module:
- **Sequencer fixes: 2 of 11 bench checks passed.** On one module, in a build that had the same sequencer code but not yet the
  calibration code (loaded 2026-10-23): the CV knob check (slow, fast and reverse sweeps behaved) and loop nesting (the expected
  stage order played). **Checks 3 to 11 have not been run.**
- **This merged image was loaded onto a real 251e on 2026-10-26** through the Xenomorpher card route (third attempt; the first two
  stalled). Afterwards the module answers the calibration status request ("no valid record"), which shows the extra flash page was
  programmed. Neither the presets nor normal sequencer playback were checked after this image was loaded; the two passed sequencer checks ran on the earlier build.
- **Three measuring-only calibration runs** were made against it, nothing written: the two logged runs agreed closely (the first, read from a photo,
  differed by 3 gain steps on one channel). In a separate test a held output released itself after 5 seconds. Details and caveats in [KNOWN-ISSUES.md](KNOWN-ISSUES.md).
- **No calibration record has ever been written to a real module with this firmware.** The write path has been exercised only in an
  emulator and by code review.
- Not measured on a module: the tempo constant (item 11), SAVE without a pause (item 18), and whether a stored record survives a
  reflash.

Please test, in this order, and report: the version after loading; the CV knob (40 slow clicks up from 0.0 read 4.0 with no backward
step; 40 back return to 0.0); a nested-loop sequence; the pulse and tempo items with a scope if you have one. Do not use the
calibration commands on a module whose presets you have not backed up.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 30.7 the same way; to return to the previous community build,
reflash [30.7C2](../30.7C2/INSTALL.md).
