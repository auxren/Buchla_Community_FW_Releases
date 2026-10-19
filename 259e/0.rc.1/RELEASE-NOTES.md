# 259e Twisted Waveform Generator — Community firmware 0.rc.1 (release candidate 1)

**Based on:** Buchla 259E firmware **31.2** (`259E_312.hex`, 11/26/2024, sha256
`556a839b2b0216bbf4e23ba596b0b7a92c202e702438018cf7c39adf5b20c096`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 31.2. The version this build reports
(the panel's version announcement on the bus) is **0.rc.1**; this is the community numbering track, as for the 272e.

**Status: release candidate.** Flashed and checked on one 259e on a live 200e bus. See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `259Ev312_0.rc.1.hex` | firmware image (Intel HEX) | `9e399539df64c81c44cc3764d269d7bbf2a6dd06f463918dc1d83cd7af0a9933` |
| `259Ev312_0.rc.1.card.bin` | the same image as a 64 KB USB-Firmware-Card image | `f8ef9d75b1d3b9dcab9282c73565bb7e861c337a04b85b9e43953bb01bb5f22e` |

The file names keep Buchla's `259Ev312…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 31.2; that is cosmetic. The module itself reports 0.rc.1.

The image occupies exactly the same flash areas as Buchla's own 31.2 update. The waveshaping tables stored elsewhere in the
module and the preset bank are not touched by the update.

## What changed (summary)
Four problems in 31.2 are fixed. Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. The panel (knobs, buttons, bus commands) could freeze permanently — audio still running — if the preset manager or bus
   master stopped acknowledging while the module was in polling mode.
2. A knob edit could reach the sound engine half-updated, giving a momentary blip, or leave a small permanent offset in a
   parameter.
3. A bus message arriving at the wrong moment could delay the audio engine past its sample period, repeating one sample.
4. Short button taps could be lost; the panel only looked at the buttons every 42 ms.

Sound, presets, the preset format, the bus protocol, card BACKUP/RESTORE and knob feel are unchanged.

## Test status
Done on hardware (one 259e, address 0x28, 200e bus with a Xenomorpher as the bus master, no preset manager):
- Flashed over the bus; the module boots, plays and answers a bus QUERY. **Pass.**
- BACKUP of the preset bank over the bus: all 30 presets read back intact. **Pass.**
- The module reports **0.rc.1** in its version announcement. **Pass.**
- Panel: quick taps on Remote and the mode / waveform / wave-select buttons all register; knobs and sound as before. **Pass.**
- After the session the bus master's counters show no errors, no dropped frames, no stuck bus.

Not yet run on hardware for this candidate: the exact freeze scenario of fix 1 (a bus master that disappears while the
module is polling), card RESTORE, SAVE / RECALL across a power cycle, and a long soak. Reports are welcome.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 31.2 the same way.
