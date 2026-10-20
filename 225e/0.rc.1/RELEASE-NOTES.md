# 225e MIDI Decoder / Preset Manager (MIDI processor, 225E) — Community firmware 0.rc.1 (release candidate 1)

**Based on:** Buchla firmware **30.9** (`225E_309_MIDI.hex`, file dated 2025-06-02 on buchla.com/download, sha256
`95ab5c4385e77b31525c99b65c6144929aa1e93f425e80b8015231e4b774f3d6`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 30.9. The version this build reports
(the module's version announcement on the bus) is **0.rc.1**; this is the community numbering track, as for the 272e and 259e.

**Status: release candidate, not yet run on hardware.** See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `225Ev309_0.rc.1.hex` | firmware image (Intel HEX) | `28b64d1d5e69e9372bfc803015e82d05528ac535d2166c0bf53f7bfa3702f2ad` |
| `225Ev309_0.rc.1.card.bin` | the same image as a 64 KB USB-Firmware-Card image | `74056c8aaf7970184a13eb4aace281a2b4437885b155f6a9d9a4d7c4883bb597` |

The file names keep Buchla's `225Ev309…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 30.9; that is cosmetic. The module itself reports 0.rc.1.

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
