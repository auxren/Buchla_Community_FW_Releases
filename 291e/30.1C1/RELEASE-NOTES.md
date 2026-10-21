# 291e Triple Morphing Filter — Community firmware 30.1C1 (release candidate 1)

**Based on:** Buchla firmware **30.1** (`291Ev301.hex`, file dated 2019-06-04 on buchla.com/download, sha256
`669ad2921da2dce72ef4915db4c90c3259a1fbd9d6aa6f5880548c90253500a2`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 30.1. The version this build reports
(the module's version announcement on the bus) is **30.1C1**; the number is Buchla's version followed by `C` (a community build made with Claude) and a revision number, so the module always says what it is based on.

**Status: release candidate, not yet run on hardware.** See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `291Ev301_30.1C1.hex` | firmware image (Intel HEX) | `8e9c81f5a84a522af604af46898c74159b4d71afc90e4e2a21546a5f53bd715c` |
| `291Ev301_30.1C1.card.bin` | the same image as a 64 KB USB-Firmware-Card image | `4366951e6d4bfacfb8bd341315ec65f1f5b7617e0043d5330422a8928955db60` |

The file names keep Buchla's `291Ev301…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 30.1; that is cosmetic. The module itself reports 30.1C1.

The image writes exactly the same flash areas as Buchla's own 30.1 update and nothing else.

## What changed (summary)
One problem in 30.1 fixed. Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. Five ways to hang the module are closed: a key code that stopped it for good, an unlimited wait for the key chip, a key buffer that erased itself when full, an unlimited wait for the display, and an unlimited wait for the bus.

Everything else, including sound, presets and the bus protocol, is unchanged.

## Test status
Not yet run on hardware. Checked in the lab only.

Reports from anyone who flashes it are welcome.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 30.1 the same way.
