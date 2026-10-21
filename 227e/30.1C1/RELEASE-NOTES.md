# 227e System Interface — Community firmware 30.1C1 (release candidate 1)

**Based on:** Buchla firmware **30.1** (`227Ev301.hex`, file dated 2019-06-04 on buchla.com/download, sha256
`368d5da765abdf7823179a552f20ab1ae51cb79feb89429cd41d95f427eb6d29`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 30.1. The version this build reports
(the module's version announcement on the bus) is **30.1C1**; the number is Buchla's version followed by `C` (a community build made with Claude) and a revision number, so the module always says what it is based on.

**Status: release candidate, flashed on one 227e.** See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `227Ev301_30.1C1.hex` | firmware image (Intel HEX) | `a6ed1c7618177ccbdafd38975aeac68f0deab9946a06979531243388ec29b31a` |
| `227Ev301_30.1C1.card.bin` | the same image as a 64 KB USB-Firmware-Card image | `7edc82acd986662478cb93c88731c8c3f64691818e9dd8ad90e21d702f6e51a0` |

The file names keep Buchla's `227Ev301…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 30.1; that is cosmetic. The module itself reports 30.1C1.

The image writes exactly the same flash areas as Buchla's own 30.1 update and nothing else.

## What changed (summary)
One problem in 30.1 is fixed. Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. A quick tap on a panel button could be missed entirely: the panel needed a button to stay down noticeably longer than a quick tap before it believed it.

Everything else, including sound, presets and the bus protocol, is unchanged.

## Test status
Flashed on one 227e on 2026-10-20 through the card route (the module read the whole image) and the owner reports it works:
boots, buttons and LEDs as before. Still to do: the short-tap comparison against stock and a long idle check.

Reports from anyone who flashes it are welcome.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 30.1 the same way.
