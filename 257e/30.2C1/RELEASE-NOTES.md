# 257e Control Voltage Processor — Community firmware 30.2C1 (release candidate 1)

**Based on:** Buchla 257E firmware **30.2** (`257Ev302.hex`, Buchla download dated 2019-06-04, sha256
`17bf45b0c5fc73d7663d7d16d8bc3c9be57b17061abff8f250becbdc0d0e860c`).
The application is byte-for-byte Buchla's 30.2 except for what is listed under [Fixed bugs](FIXED-BUGS.md). The version this build
reports (the module's version announcement on the bus) is **30.2C1**; the number is Buchla's version followed by `C` (a community build made with Claude) and a revision number, so the module always says what it is based on.

**Status: pre-release (release candidate 1), flashed on one module 2026-11-19; the fixes themselves are not yet checked on hardware.** See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `257Ev302_30.2C1.hex` | firmware image (Intel HEX) | `cdb576140bc386cd9af3470dddc773b0a62e80ebc39001a00af1bb755d13ebf0` |
| `257Ev302_30.2C1.card.bin` | the same image as a 224 KB firmware-card image (the larger card layout used by the 200e's 32-bit modules) | `d9083f7826d78834c1cdc87a24ef2be3163dd96d3bef9e29aca1bb3f587daf9c` |

The file names keep Buchla's `257Ev302…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 30.2; that is cosmetic. The module itself reports 30.2C1.

**Two differences from Buchla's file in what the image covers** (see [INSTALL.md](INSTALL.md#what-the-image-covers)):
- Buchla's `257Ev302.hex` also contains 32 KB for the area in front of the application, where the module's loader lives. This
  image contains the application only and leaves that area alone, like Buchla's files for the other 32-bit modules.
- It adds 24 bytes of code in previously unused space, inside a flash page Buchla's update already writes.

## What changed (summary)
Three robustness fixes; nothing about how the module processes voltages or what its panel does. Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. A preset **SAVE or RECALL sent over the bus for a slot beyond the module's 30** is now ignored. Before, the module acted on any
   slot number: a SAVE could write outside its preset memory and a RECALL could load meaningless values as the live settings.
2. The **reply the module sends after loading a preset** ended in an accidental byte (whatever happened to be in memory). It now
   ends in the module's own address.
3. A **bus message arriving while a button press or timer event was being queued** could corrupt that event. It no longer can.

Everything else, including the control-voltage processing, the pots, the buttons and the presets themselves, is unchanged.

## Test status
**Loaded on one 257e on 2026-11-19**, from a card stand-in (a Xenomorpher serving the card image), not from Buchla's own USB
Firmware Card. This was the first load of a 257e by that route. The module, which announced 30.2 beforehand, read the card in a
single pass (the 257e programs itself as it reads; there is no second pass), came back up after a power cycle and answers on
the bus. It reports **30.2C1**, as read by its owner on the display of the device that listens to the module's version announcement.

**Not checked on hardware:**
- any of the three fixes (they were checked in the lab only);
- saving and recalling presets from a preset manager after the update;
- long use;
- Buchla's own USB Firmware Card route.

Reports from anyone who flashes it are welcome.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 30.2 the same way.
