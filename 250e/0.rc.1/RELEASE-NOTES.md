# 250e Dual Arbitrary Function Generator — Community firmware 0.rc.1 (release candidate 1)

**Based on:** Buchla 250E firmware **30.6b1** (`250Ev306b1.hex`, 2019-06-04, a Buchla beta, sha256
`b388f9b0cd7a7f739838ccb1010252c27daa2df46db1e3b7208f74d1d3cd2a2e`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 30.6b1. The version this build reports
(the panel's version announcement on the bus) is **0.rc.1**; this is the community numbering track, as for the 259e and 272e.

**Status: release candidate, not yet run on hardware.** See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `250Ev306b1_0.rc.1.hex` | firmware image (Intel HEX) | `fd20c3a4e73c81da48c9d833cd2926519b13cecb54be5513b156b6e6b6b62d71` |
| `250Ev306b1_0.rc.1.card.bin` | the same image as a 64 KB USB-Firmware-Card image | `e859dc2f137565ac67443c9b9ee65a97f59117d39bbe69bfb84ea534ed7399b0` |

The file names keep Buchla's `250Ev306b1…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 30.6b1; that is cosmetic. The module itself reports 0.rc.1.

The image occupies exactly the same flash areas as Buchla's own 30.6b1 update; nothing is written anywhere else. The preset
bank is not touched by the update.

## What changed (summary)
One problem in 30.6b1 is fixed. Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. Turning the encoder quickly skipped steps, and a fast flick could even move the stage cursor or value the wrong way.

Sound, presets, the preset format, the bus protocol, card BACKUP/RESTORE, button timing and the feel of a slow, deliberate
turn are unchanged.

## Test status
**Not yet run on hardware. Checked in the lab only.** Nothing in this release has been flashed to a module. Reports from
owners who try it are welcome; see [KNOWN-ISSUES.md](KNOWN-ISSUES.md) for what to watch for.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own firmware (30.5 or 30.6b1) the same way.
