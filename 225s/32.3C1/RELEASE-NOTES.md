# 225e MIDI Decoder / Preset Manager (storage/card processor, 225S) — Community firmware 32.3C1 (release candidate 1)

**Based on:** Buchla firmware **32.3** (`225Sv323_Primo.hex`, file dated 2019-06-04 on buchla.com/download, sha256
`f651a8bf58f13c001bb7ac46a3d6fdefd95282d863e13c7cb6657f769efdec3d`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 32.3. The version this build reports
(the module's version announcement on the bus) is **32.3C1**; the number is Buchla's version followed by `C` (a community build made with Claude) and a revision number, so the module always says what it is based on.

**Status: release candidate, not yet run on hardware.** See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `225Sv323_32.3C1.hex` | firmware image (Intel HEX) | `c79d47cb40b7e158f8576f55d4f7cb4b8c3272fa7f8f836e6428b85027e99d37` |
| `225Sv323_32.3C1.card.bin` | the same image as a 64 KB USB-Firmware-Card image | `012d3d1cedf599efc71acbb5178b08ce5d8dbb19de5e610d3158c8808c0104c0` |

The file names keep Buchla's `225Sv323…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 32.3; that is cosmetic. The module itself reports 32.3C1.

The image writes exactly the same flash areas as Buchla's own 32.3 update and nothing else.

## What changed (summary)
One problem in 32.3 is fixed. Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. The encoder could lose a click, more often on a worn or bouncy encoder.

Everything else, including sound, presets and the bus protocol, is unchanged.

## Test status
Not yet run on hardware. Checked in the lab only.

Reports from anyone who flashes it are welcome.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 32.3 the same way.
