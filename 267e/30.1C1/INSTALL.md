# Installing 267e 30.1C1

## Check your version first
Hold the 267e's **Remote Enable** button for a few seconds with a preset manager polling the bus: the module announces its
version and the preset manager shows it.
- **30.1** (or earlier): this build applies.
- **30.2**: **do not install.** 30.2 is not available anywhere we know of, this build would replace it, and you could not go back.

**Before you start:** take a BACKUP of your presets if you want to keep them (loading this firmware erases the module's 30
presets) and keep Buchla's own 267E 30.1 (from buchla.com) on hand so you can go back. Read the version your module announces
first; if it is newer than 30.1, this build will replace it with the 30.1-based one. Do not flash while the 200e system is under
power if your tool warns you not to.

**Never program the module's chip directly with a debug adapter** (a Silicon Labs USB Debug Adapter with SiUtil or the
Flash Programming Utility, an Atmel/Microchip JTAG tool, or any other JTAG/C2 programmer). Buchla locks the module's flash at the
factory; those tools can only get past the lock by erasing the whole chip, which destroys the module's bootloader, its factory
tables and calibration, and its presets. The files here are meant only for the USB Firmware Card route or a device that stands in
for the card, as described below.

## With Buchla's USB Firmware Card (the standard route)
1. Power off the 200e system. Connect the USB Firmware Card to your computer.
2. In Buchla's firmware utility, load `267Ev301_30.1C1.hex` onto the card. The file name keeps Buchla's pattern so the utility
   reads the module and version from it. Wait for the card LED to finish.
3. Put the card in the 200e card slot.
4. Power on the system **while holding the 267e's Remote Enable button**; keep holding until the module's LEDs change.
5. Wait one to two minutes for the module to program itself, then power-cycle the system normally.
6. Check the module announces **30.1C1** (with a preset manager polling, hold Remote Enable for several seconds).

## With a device that stands in for the card (the route this image has been loaded by)
`267Ev301_30.1C1.card.bin` is the same image laid out as a 224 KB firmware-card image of the larger layout used by the 200e's
32-bit modules. It needs a card stand-in that supports that larger card (three-byte addressing); the 64 KB stand-ins used for the
8-bit modules cannot serve it. Write it to the stand-in (for example a Xenomorpher serving it as its firmware card; the stand-in must be running and serving
before the 267e powers up), then follow steps 4-6 above. The 267e reads the card once, in about 45 seconds, and programs itself
as it reads. The USB Firmware Card route above has not been tried with this image.

## Verify your download
`shasum -a 256 -c SHA256SUMS`

## Going back
There is no way back to 30.2. Reflash Buchla's own 267E 30.1 the same way (load its `.hex` on the card and power on holding Remote Enable). The presets are
erased by either load.
