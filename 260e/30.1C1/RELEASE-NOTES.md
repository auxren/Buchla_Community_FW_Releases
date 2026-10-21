# 260e Duophonic Pitch Class Generator — Community firmware 30.1C1 (release candidate 1)

**Based on:** Buchla firmware **30.1** (`260Ev301.hex`, file dated 2019-06-04 on buchla.com/download, sha256
`c49fcc17d0647a30803f3544c573065a4ab9772aa12d21caef663c6afe0075b6`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 30.1. The version this build reports
(the module's version announcement on the bus) is **30.1C1**; the number is Buchla's version followed by `C` (a community build made with Claude) and a revision number, so the module always says what it is based on.

**Status: release candidate, not yet run on hardware.** See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `260Ev301_30.1C1.hex` | firmware image (Intel HEX) | `9f9e0e289c16ee72f05f441678f1e7b203c487de7dd233aaed4b9cec2124e04a` |
| `260Ev301_30.1C1.card.bin` | the same image as a 64 KB USB-Firmware-Card image | `be71b8b6c2a7ace70273f0c026670cf68958ee8e1614c0e8946bc794b410346f` |

The file names keep Buchla's `260Ev301…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 30.1; that is cosmetic. The module itself reports 30.1C1.

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
