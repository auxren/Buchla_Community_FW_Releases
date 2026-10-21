# 210e Control & Signal Router — Community firmware 30.5AC1 (release candidate 1)

**Based on:** Buchla firmware **30.5A** (`210Ev305A_SSM.hex`, file dated 2024-07-16 on buchla.com/download, sha256
`1a1334cf957cde9a12ab5768a6d75f947c6266611b275cf75da6119643c66362`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 30.5A. The version this build reports
(the module's version announcement on the bus) is **30.5AC1**; the number is Buchla's version followed by `C` (a community build made with Claude) and a revision number, so the module always says what it is based on.

**Status: release candidate, not yet run on hardware.** See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `210Ev305A_30.5AC1.hex` | firmware image (Intel HEX) | `c805258cbba96eb5035dbfe94241dbe4187f1c7ac58159699d05f6359b09ae92` |
| `210Ev305A_30.5AC1.card.bin` | the same image as a 64 KB USB-Firmware-Card image | `66eff948601698b89e485005bc04dcc598922bde9c2a9af1e831e91169bcebfd` |

The file names keep Buchla's `210Ev305A…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 30.5A; that is cosmetic. The module itself reports 30.5AC1.

The image writes exactly the same flash areas as Buchla's own 30.5A update and nothing else.

## What changed (summary)
One problem in 30.5A fixed. Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. Turning a rotary encoder quickly could skip steps, and now and then register a step in the wrong direction. The module did not listen to its encoders during a large part of each of its internal update cycles, and again while it redrew its display.

Everything else, including sound, presets and the bus protocol, is unchanged.

## Test status
Not yet run on hardware. Checked in the lab only.

Reports from anyone who flashes it are welcome.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 30.5A the same way.
