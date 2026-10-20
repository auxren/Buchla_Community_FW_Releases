# 227e System Interface — Community firmware 0.rc.1 (release candidate 1)

**Based on:** Buchla firmware **30.1** (`227Ev301.hex`, file dated 2019-06-04 on buchla.com/download, sha256
`368d5da765abdf7823179a552f20ab1ae51cb79feb89429cd41d95f427eb6d29`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 30.1. The version this build reports
(the module's version announcement on the bus) is **0.rc.1**; this is the community numbering track, as for the 272e and 259e.

**Status: release candidate, not yet run on hardware.** See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `227Ev301_0.rc.1.hex` | firmware image (Intel HEX) | `3a7b07c067f39e15baf15e86c4cb59d508eacb79df185b0d93d398cf9546a848` |
| `227Ev301_0.rc.1.card.bin` | the same image as a 64 KB USB-Firmware-Card image | `8867de817e3d5b84fea32af1925f252a7c2be6caa3c44b72dcddbe10e4d939c9` |

The file names keep Buchla's `227Ev301…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 30.1; that is cosmetic. The module itself reports 0.rc.1.

The image writes exactly the same flash areas as Buchla's own 30.1 update and nothing else.

## What changed (summary)
One problem in 30.1 is fixed. Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. A quick tap on a panel button could be missed entirely: the panel needed a button to stay down noticeably longer than a quick tap before it believed it.

Everything else, including sound, presets and the bus protocol, is unchanged.

## Test status
Not yet run on hardware. Checked in the lab only.

Reports from anyone who flashes it are welcome.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 30.1 the same way.
