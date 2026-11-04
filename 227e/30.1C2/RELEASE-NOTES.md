# 227e System Interface — Community firmware 30.1C2 (release candidate 2)

**Based on:** Buchla firmware **30.1** (`227Ev301.hex`, file dated 2019-06-04 on buchla.com/download, sha256
`368d5da765abdf7823179a552f20ab1ae51cb79feb89429cd41d95f427eb6d29`), plus the button fix from [30.1C1](../30.1C1/RELEASE-NOTES.md).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) or below is byte-for-byte Buchla's 30.1 (with 30.1C1's button change). The version this build reports
(the module's version announcement on the bus) is **30.1C2**; the number is Buchla's version followed by `C` and a revision number, so the module always says what it is based on.

**Status: pre-release (release candidate 2), tested on one module.** Pan mode and saving it in a preset were seen
working by the owner; the voltages, the knob behaviour and long-term use have not been measured. See [Test status](#test-status).
It is not a stable release.

## Files
| file | what | sha256 |
|---|---|---|
| `227Ev301_30.1C2.hex` | firmware image (Intel HEX) | `e29b7f46845f8a328a8a0126f111913bf8b0cf1139ebd7e7d1668a938822155c` |
| `227Ev301_30.1C2.card.bin` | the same image as a 64 KB firmware-card image | `9773bd76e3cd497afcd5701c1216776eea9201aaac7afc9361e8bd825ce8d43f` |

The file names keep Buchla's `227Ev301…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 30.1; that is cosmetic. The module itself reports 30.1C2.

**This image writes two flash pages that Buchla's own update never writes** (addresses `0x3400` and `0x3600`, both inside the area
the module's loader erases and rewrites during any update). See [INSTALL.md](INSTALL.md) and [KNOWN-ISSUES.md](KNOWN-ISSUES.md).

## What changed (summary)
Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. **Pan mode (new).** Hold a swirl button for about 0.8 s and that input switches to pan mode: the swirl LED blinks about twice a second.
   - The **rate** input becomes a position control over the four outputs in the order C, A, B, D:
     0 V = about 100 % C, 3.33 V = about 100 % A, 6.67 V = about 100 % B, 10 V = about 100 % D. Between two neighbours the two are mixed linearly
     (about -6 dB on each side at the midpoint between them).
   - The **ampl** input becomes a slew limiter on the rate input: it sets how slowly the position follows a change. The glide time for a full
     0 to 10 V move runs from instant to about 17 s.
   - The **rate and ampl knobs** are plain attenuators of their inputs in pan mode. With a knob fully counter-clockwise its input adds
     nothing (for the rate knob that means the position stays at 100 % C); the top of the knob range is treated as fully clockwise.
   - Hold the button again to leave pan mode; the LED goes off and the input is in standard mode (it does not return to swirl).
   - Pan mode is saved in presets and restored when a preset is recalled, and at power-up if slot 0 holds it. Presets made before are unaffected.
2. **A short swirl-button press now acts when the button is released**, not when it goes down (needed to tell a short press from a hold).
3. **RESTORE no longer writes a stale slot when a card read fails.** It tries each read up to 4 times, then stops without writing
   that slot or the later ones. It still sends its normal completion reply, so the host cannot tell; read the bank back after a restore.
4. **Block-move (0x07) and exchange (0x08) bus commands refuse out-of-range slot numbers**, so they can no longer loop forever or write past slot 29.
5. Carries 30.1C1's faster button qualifier (taps from about 11 ms; the processor runs at 24.5 MHz, so the panel look interval is
   10.7 ms, as corrected in the [30.1C1 notes](../30.1C1/KNOWN-ISSUES.md)).

Everything else, including sound, the other buttons, presets of the standard modes and the rest of the bus protocol, is unchanged.

## Test status
**Loaded on one 227e on 2026-11-04**, from a card stand-in (a Xenomorpher serving the card image), not from Buchla's own USB Firmware Card.
The first attempt stalled at the loader's fixed 80-byte header read and wrote nothing (the module kept its old firmware); the second attempt
completed. The cause of the stall is not established. The preset bank read back identical before and after the load.

What the owner then confirmed on that module:
- the version reads **30.1C2**;
- pan mode works (hold a swirl button: the LED blinks, the rate input moves the signal between the outputs and the ampl input slows it, judged by ear and not metered);
- the pan state is saved by a preset store and comes back on recall.

A listening check for clicks from the blinking LED found none so far.

**Not checked:**
- the exact voltage points (0, 3.33, 6.67, 10 V) and how well the outputs separate there, with a meter;
- the attenuator behaviour of the two knobs along their travel (the direction of the knobs is a design assumption);
- the slew times against the stated range;
- the 0.8 s hold time and the blink rate with a clock (they are calculated from the processor clock as decoded from the code, not measured);
- behaviour on the other hardware variant of the module;
- how it behaves in long use, with several inputs in pan mode and moving CVs;
- the RESTORE and block-move changes on a module (they were checked in an emulator of the firmware only);
- Buchla's own USB Firmware Card route (not tried);
- panel-switch bounce against the button qualifier.

Reports from anyone who flashes it are welcome.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return, reflash Buchla's own 30.1 or [30.1C1](../30.1C1/RELEASE-NOTES.md) the same way.
