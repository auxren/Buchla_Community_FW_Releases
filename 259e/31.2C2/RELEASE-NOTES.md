# 259e Twisted Waveform Generator — Community firmware 31.2C2 (release candidate 2)

**Based on:** Buchla 259E firmware **31.2** (`259E_312.hex`, 11/26/2024, sha256
`556a839b2b0216bbf4e23ba596b0b7a92c202e702438018cf7c39adf5b20c096`), via community
[31.2C1](../31.2C1/RELEASE-NOTES.md). Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 31.2.
The version this build reports (the panel's version announcement on the bus) is **31.2C2**.

**Status: release candidate.** Flashed and checked on one 259e on a live 200e system, including the new power-up selection
and the Original-table mode. See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `259Ev312_31.2C2.hex` | firmware image (Intel HEX) | `7fb16b3219d95c35ec434f75e0a906377cd266d871fcedfcd5856ee8442a96fa` |
| `259Ev312_31.2C2.card.bin` | the same image as a 64 KB USB-Firmware-Card image | `c08e2f22fe5305221876a1e5e3c7dd206b867d1ee2c0a397cdfdcf3c0754e182` |

The file names keep Buchla's `259Ev312…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 31.2; that is cosmetic. The module itself reports 31.2C2.

The image occupies exactly the same flash areas as Buchla's own 31.2 update. The waveshaping tables stored elsewhere in the
module and the preset bank are not touched by the update.

## What changed (summary)
31.2C2 adds one feature on top of the four fixes of 31.2C1 (details in [FIXED-BUGS.md](FIXED-BUGS.md)):

**Original wavetables, selectable at power-up.** The 259e carries fourteen factory transfer tables in its flash; the Twisted
firmware uses eight of them (timbres 1 to 4 on each side) and turns the a, b and c positions into memory scans. Holding
**TIMBRE** while powering up now boots the module with a, b and c pointing at the six factory tables the Twisted firmware does
not use, the ones from the original 259e. In that mode the FM knobs act as FM for a, b and c, as they did on the original,
and the memory-scan indication stays off. Powering up without the button (or holding the SHAPE button) boots the
normal Twisted behaviour. The choice is not remembered: it is made at every power-up. Timbres 1 to 5, presets, the preset
format, the bus protocol, card BACKUP/RESTORE and knob feel are unchanged.

## Test status
Done on hardware (one 259e on a live 200e bus, 2026-10-20):
- 31.2C2 flashed; the module boots, plays, answers a bus QUERY and reports **31.2C2** in its version announcement. **Pass.**
- Power-up with nothing held: the Twisted behaviour of 31.2C1 / 31.2. **Pass.**
- Power-up with TIMBRE held: the Original-table mode, with a, b and c on the factory tables. **Pass.**
- Carried over from 31.2C1 (same code): preset BACKUP, panel taps, knobs and sound. **Pass.**

Reports from owners are still welcome on the finer points: what the timbre LEDs show for a, b and c in Original mode, and
whether the order of the three original tables per side matches the original 259e (see [Known issues](KNOWN-ISSUES.md)).

Also still open from 31.2C1: the exact freeze scenario of fix 1, card RESTORE, SAVE / RECALL across a power cycle, long soak.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 31.2 the same way.
