# 225e MIDI Decoder / Preset Manager (storage/card processor, 225S) — Community firmware 0.rc.1 (release candidate 1)

**Based on:** Buchla firmware **32.3** (`225Sv323_Primo.hex`, file dated 2019-06-04 on buchla.com/download, sha256
`f651a8bf58f13c001bb7ac46a3d6fdefd95282d863e13c7cb6657f769efdec3d`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 32.3. The version this build reports
(the module's version announcement on the bus) is **0.rc.1**; this is the community numbering track, as for the 272e and 259e.

**Status: release candidate, not yet run on hardware.** See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `225Sv323_0.rc.1.hex` | firmware image (Intel HEX) | `f83bc0432505d87c277146de0e1b7581455278f7c01feb9d4aa20e21a4a153f2` |
| `225Sv323_0.rc.1.card.bin` | the same image as a 64 KB USB-Firmware-Card image | `557214ee81e5227c76649550854f87ea6ea983f795664899b7145bff544597c5` |

The file names keep Buchla's `225Sv323…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 32.3; that is cosmetic. The module itself reports 0.rc.1.

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
