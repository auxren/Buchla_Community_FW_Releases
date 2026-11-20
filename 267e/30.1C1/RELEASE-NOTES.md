# 267e Dual Random Voltage Generator: Community firmware 30.1C1 (release candidate 1)

**Based on:** Buchla firmware **30.1** (`267Ev301.hex`, sha256 `3d9294f79fbae5b51c57e4ca82aa5ac21f11adfec426130a256b6f5b8f76ce3f`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 30.1. The version this build reports
(the module's version announcement on the bus) is **30.1C1**; the number is Buchla's version followed by `C` (a community build
made with Claude) and a revision number, so the module always says what it is based on.

**Status: release candidate, flashed and checked on one 267e.** See [Test status](#test-status).

> **If your 267e reports version 30.2, do not install this.** This build is made from Buchla's published 30.1. Some modules carry a
> later firmware, 30.2, which is not among Buchla's downloads and which we do not have. Installing this build replaces it, there is
> no way back to 30.2, and we do not know what 30.2 changed (it may already contain Buchla's own fix for the bug below). The module
> this build was loaded on reported 30.2 beforehand, and that firmware is gone from it. Check your module's version first; see
> [INSTALL.md](INSTALL.md#check-your-version-first).

## Files
| file | what | sha256 |
|---|---|---|
| `267Ev301_30.1C1.hex` | firmware image (Intel HEX) | `3d8186f471e605664bb316dffc803368400c6bb1b69bdd066aa449ca1d4feca9` |
| `267Ev301_30.1C1.card.bin` | the same image as a 224 KB USB-Firmware-Card image | `66b096bf4931d603edfd4421ec78405f2862b51f6886eda82e900c80f610cfe4` |

The file names keep Buchla's `267Ev301…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 30.1; that is cosmetic. The module itself reports 30.1C1.

## What changed (summary)
Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. The "external c.v. <-> random" mix pot of each random section (A and B) is now saved with a preset and recalled with it, like
   the module's other pots. Before, it always followed the panel position and ignored what the preset held.
2. The two stored mix values can no longer push the mix outside its range if a preset record is damaged.
3. The module reports `30.1C1`.

Everything else, including sound, the bus protocol and the other pots, is unchanged.

## Test status
Flashed on one 267e on 2026-11-19 from a card stand-in (a Xenomorpher serving the card image; the module read the card in a
single pass of about 45 seconds), not from Buchla's own USB Firmware Card; the module announces **30.1C1**, and the external c.v. <-> random mix
pot is saved with a preset and recalled. **Pass, on one module.** Not yet done: a long soak. Reports from anyone who flashes it are welcome.

## Before you load it
**Loading firmware erases the module's 30 presets.** Take a BACKUP first if you want them. Stock Buchla 267E **30.1** remains
available from Buchla and is the way back. A module that shipped with a newer factory firmware than 30.1 (some report 30.2) will
lose whatever that newer firmware changed, because this build is based on 30.1; read the version your module announces before
you load.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 30.1 the same way.
