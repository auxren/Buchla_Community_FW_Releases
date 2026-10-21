# 272e Polyphonic Tuner — Community firmware 31.0C1 (release candidate 1)

**Based on:** Buchla 272E firmware **31.0b1** (`272Ev310b1.hex`, sha256 `dd2695636cf38f575ed385cc1824752ddb19760ce741eb8dc165f140aa143a21`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 31.0b1. The version this build reports
(key code 22 and the module announcement on the bus) is **31.0C1**; the number is Buchla's version followed by `C` (a community build made with Claude) and a revision number, so the module always says what it is based on.

**Status: release candidate.** Tested on one 272e on a live 200e system. See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `272Ev310b1_31.0C1.hex` | firmware image (Intel HEX) | `69abff4568452a2a18987db44648795a4857cd379cec2ff794da1126b0937a93` |
| `272Ev310b1_31.0C1.card.bin` | the same image as a 64 KB USB-Firmware-Card image | `56d5b26ddc9a6f540a413d079da4456c4d9ab7e547d94bd7eb350be0ac6ca695` |

The file names keep Buchla's `272Ev310…` naming pattern because Buchla's flashing tools read the module and version from it.
The card image's header therefore still shows version 31.0; that is cosmetic. The module itself reports 31.0C1.

## What changed (summary)
Seven problems in 31.0b1 are fixed, all of them cases where the module could lag, freeze or lock up. Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. About 2 s of frozen display and LEDs after turning a tuner knob quickly.
2. Lag after pressing Remote or other panel controls.
3. Possible permanent lock-up when the 200e bus is slow, busy or stuck (three places).
4. A stray panel key code 23 halted the module until power-cycled.
5. A stuck panel-encoder line could freeze the whole module.
6. A burst of more than 127 panel events could wipe the whole event queue.
7. Card BACKUP / RESTORE could hang the module waiting on a stuck bus (four places).

No function, panel behaviour or preset format was changed.

## Test status
Tested on hardware (one module, 200e bus with a Xenomorpher as the bus master, antenna fitted):
- Fast knob spins: display and LEDs stay responsive, and the radio ends on the displayed frequency. **Pass.**
- Preset RECALL over the bus. **Pass** (see [Known issues](KNOWN-ISSUES.md) for the polling-complete requirement).
- The released image itself, under its previous number `0.rc.1`: the module reported 0.rc.1, boots normally, and SAVE and RECALL still work. **Pass.** (Since renumbered 31.0C1; only the version bytes differ, and that string has not been checked on a module yet.)

Checked against Buchla's 31.0b1: the image differs only in the intended places and the preset flash page is untouched.

Not yet run on hardware for this candidate: all four tuners and two knobs at once, every panel control and the frequency
limits, SAVE/RECALL across a power cycle, BACKUP then RESTORE of the bank, and a long soak. Reports are welcome.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 31.0b1 the same way.
