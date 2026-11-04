# Installing 227e 30.1C2

**Before you start:** take a BACKUP of your presets if your system has any (put the 227e in Remote Enable first; a backup that comes back empty has
failed), and keep Buchla's own 30.1 (`227Ev301.hex` from buchla.com) or [30.1C1](../30.1C1/INSTALL.md) on hand so you can go back.
This is a pre-release; flash it only on a module you can afford to reflash. Do not flash while the 200e system is under power if your tool warns you not to.

**Never program the module's chip directly with a debug adapter** (a Silicon Labs USB Debug Adapter with SiUtil or the
Flash Programming Utility, an Atmel/Microchip JTAG tool, or any other JTAG/C2 programmer). Buchla locks the module's flash at the
factory; those tools can only get past the lock by erasing the whole chip, which destroys the module's bootloader, its factory
tables and calibration, and its presets. The files here are meant only for the firmware-card route or a device that stands in
for the card, as described below.

## With Buchla's USB Firmware Card
**This route has not been tried with this image** (see the extra pages below).
1. Power off the 200e system. Connect the USB Firmware Card to your computer.
2. In Buchla's firmware utility, load `227Ev301_30.1C2.hex` onto the card. The file name keeps Buchla's pattern so the utility reads
   the module and version from it. Wait for the card LED to finish.
3. Put the card in the 200e card slot.
4. Power on the system **while holding the module's firmware-load button (Remote Enable on most modules; check Buchla's instructions for yours)**; keep holding until the module's LEDs change.
5. Wait one to two minutes for the module to program itself, then power-cycle the system normally.
6. Check the module's version announcement on the bus reads **30.1C2** (hold Remote Enable; with a preset manager attached the version appears on the bus).

## With a device that stands in for the card (the route this image has been loaded by)
`227Ev301_30.1C2.card.bin` is the same image laid out as a 64 KB firmware-card image (the card's data starts at offset `0x50`).
Write it to whatever stands in for the card, then follow steps 4 to 6 above. On the one occasion this image was loaded this way
(a Xenomorpher serving the card), the first attempt stalled at the loader's first read (its fixed 80-byte header read) with nothing written,
and the second completed; the module kept its old firmware after the stalled attempt. If your stand-in has progress counters, they should reach
about 34,465 read transactions for this image. Stop serving the card (disarm your stand-in) before you press Remote Enable again, including for step 6. While a stand-in is still serving the card, a Remote press can act as a preset SAVE that overwrites slot 0 (the preset loaded at power-up) with the current panel settings; on the one load so far this happened once and changed slot 0.

## The extra flash pages
Buchla's update programs only some of the flash. This image also programs two pages that Buchla's update never writes (`0x3400` and `0x3600`),
which hold the pan code. They lie inside the area (`0x0800` to `0x39FF`) that the module's loader erases and rewrites during any update, so the loader
is expected to program them like the rest. That is confirmed on one module through the card stand-in route. It has not been checked whether Buchla's
firmware utility puts the whole image on the USB card. The preset bank page is not written by the update.

## If a load goes wrong
From the loader's code (not yet shown by interrupting a load): the loader sits in a locked area no update erases, and powering on with Remote Enable held and a card in the slot starts a new load, so a failed load should be redoable. On the bench, a load that stalled before erasing kept the old firmware and the retry succeeded. Rollback: a card made from Buchla's 30.1 or [30.1C1](../30.1C1/INSTALL.md) (not yet loaded over 30.1C2).

## Verify your download
Compare the files with `SHA256SUMS`:
`shasum -a 256 -c SHA256SUMS`

## Going back
Reflash Buchla's own 30.1, or 30.1C1, the same way (load its `.hex` on the card and power on holding the same button).
Read [the downgrade caveat](KNOWN-ISSUES.md#going-back-to-301-or-301c1-with-pan-presets) first if you stored pan presets.
