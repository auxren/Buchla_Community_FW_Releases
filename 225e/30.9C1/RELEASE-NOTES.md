# 225e MIDI Decoder / Preset Manager (MIDI processor, 225E) — Community firmware 30.9C1 (release candidate 1)

**Based on:** Buchla firmware **30.9** (`225E_309_MIDI.hex`, file dated 2025-06-02 on buchla.com/download, sha256
`95ab5c4385e77b31525c99b65c6144929aa1e93f425e80b8015231e4b774f3d6`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 30.9. The version this build reports
(the module's version announcement on the bus) is **30.9C1**; the number is Buchla's version followed by `C` (a community build made with Claude) and a revision number, so the module always says what it is based on.

**Status: release candidate, not yet run on hardware.** See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `225Ev309_30.9C1.hex` | firmware image (Intel HEX) | `a138a4914a14450d7a25f10ff53da25ec6f5aa88c826765f7d789c3525871ac0` |
| `225Ev309_30.9C1.card.bin` | the same image as a 64 KB USB-Firmware-Card image | `d61e0506f1f719a7a86f19b3c7f8f3a455dedd983bb09bf3232735e2c825f934` |

The file names keep Buchla's `225Ev309…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 30.9; that is cosmetic. The module itself reports 30.9C1.

The image writes exactly the same flash areas as Buchla's own 30.9 update and nothing else.

## What changed (summary)
Two problems in 30.9 are fixed. Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. The encoder could lose a click, more often on a worn or bouncy encoder.
2. The first encoder click after power-up, before anything else had been touched, could make the module restart its display start-up.

Everything else, including sound, presets and the bus protocol, is unchanged.

## Test status
Not yet run on hardware. Checked in the lab only.

Reports from anyone who flashes it are welcome.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 30.9 the same way.
