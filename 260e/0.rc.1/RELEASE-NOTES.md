# 260e Duophonic Pitch Class Generator — Community firmware 0.rc.1 (release candidate 1)

**Based on:** Buchla firmware **30.1** (`260Ev301.hex`, file dated 2019-06-04 on buchla.com/download, sha256
`c49fcc17d0647a30803f3544c573065a4ab9772aa12d21caef663c6afe0075b6`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 30.1. The version this build reports
(the module's version announcement on the bus) is **0.rc.1**; this is the community numbering track, as for the 272e and 259e.

**Status: release candidate, not yet run on hardware.** See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `260Ev301_0.rc.1.hex` | firmware image (Intel HEX) | `1f399646eb741716d7b8747ef7f4aeee80f3a0d2926e0bd61c21154728475cb0` |
| `260Ev301_0.rc.1.card.bin` | the same image as a 64 KB USB-Firmware-Card image | `20d313f5d70e0203fec22c4b0c679f161ea62867c7b2d419b2db35e73e9740ac` |

The file names keep Buchla's `260Ev301…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 30.1; that is cosmetic. The module itself reports 0.rc.1.

The image writes exactly the same flash areas as Buchla's own 30.1 update and nothing else.

## What changed (summary)
One problem in 30.1 fixed. Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. The module could freeze completely (display, buttons, everything but the sound) if the 200e bus misbehaved while it was sending a message after a long button press, or when it was about to start a message.

Everything else, including sound, presets and the bus protocol, is unchanged.

## Test status
Not yet run on hardware. Checked in the lab only.

Reports from anyone who flashes it are welcome.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 30.1 the same way.
