# 252e Polyphonic Rhythm Generator — Community firmware 0.rc.1 (release candidate 1)

**Based on:** Buchla 252E firmware **30.2** (`252Ev302.hex`, Buchla download dated 2019-06-04, sha256
`c159c03beeded16e2e1eee45a38529ec98174b6725715a91167ed6f4fdde64a6`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 30.2. The version this build reports
(the panel's version announcement on the bus) is **0.rc.1**; this is the community numbering track, as for the 259e and 272e.

**Status: release candidate, not yet run on hardware.** See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `252Ev302_0.rc.1.hex` | firmware image (Intel HEX) | `def66e4fc5a4b0695fad6f9a03728fce45ee3c97d0efa91f6b9e01f20632bf77` |
| `252Ev302_0.rc.1.card.bin` | the same image as a 224 KB firmware-card image (the larger card layout used by the 200e's 32-bit modules) | `660799ce4f7d81273813ff7748e94de62bd14c9d1a90a68906839764d606e9ef` |

The file names keep Buchla's `252Ev302…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 30.2; that is cosmetic. The module itself reports 0.rc.1.

The image occupies exactly the same flash areas as Buchla's own 30.2 update. The preset bank is not touched by the update.

## What changed (summary)
Two problems in 30.2 are fixed, with a very small change. Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. Turning a panel knob quickly stopped it producing steps at all (above roughly 100 steps per second); it now keeps moving,
   though a very hard spin is still thinned out (see [KNOWN-ISSUES.md](KNOWN-ISSUES.md)).
2. After tapping one of the six lockout-protected buttons (including the two knob push switches), a second tap within a fifth of a
   second was ignored. The wait is now about 40 ms.

Sound, CV outputs, presets, the preset format, the bus protocol and card BACKUP/RESTORE are unchanged.

## Test status
**Not yet run on hardware. Checked in the lab only.** No module has been flashed with this image. Not tried on a real 252e: the
fast-spin behaviour, two knobs together, double clicks of the knob push switches, or a long soak. Reports are welcome.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 30.2 the same way.
