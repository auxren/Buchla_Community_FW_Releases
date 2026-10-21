# Installing 259e 31.2C3

**Before you start:** take a BACKUP of your presets, and keep Buchla's own 259E 31.2 (from buchla.com) on hand so you can
go back. Do not flash while the 200e system is under power if your tool warns you not to.

**Never program the module's chip directly with a debug adapter** (a Silicon Labs USB Debug Adapter with SiUtil or the
Flash Programming Utility, an Atmel/Microchip JTAG tool, or any other JTAG/C2 programmer). Buchla locks the module's flash at the
factory; those tools can only get past the lock by erasing the whole chip, which destroys the module's bootloader, its factory
tables and calibration, and its presets. The files here are meant only for the USB Firmware Card route or a device that stands in
for the card, as described below.

## With Buchla's USB Firmware Card (the standard route)
1. Power off the 200e system. Connect the USB Firmware Card to your computer.
2. In Buchla's firmware utility, load `259Ev312_31.2C3.hex` onto the card. The file name keeps Buchla's pattern so the utility
   reads the module and version from it. Wait for the card LED to finish.
3. Put the card in the 200e card slot.
4. Power on the system **while holding the 259e's Remote Enable button**; keep holding until the module's LEDs change.
5. Wait one to two minutes for the module to program itself, then power-cycle the system normally.
6. Check the module announces **31.2C3** (with a preset manager polling, hold Remote for half a second).

## With a device that stands in for the card
`259Ev312_31.2C3.card.bin` is the same image laid out as a 64 KB firmware-card image (the card's data starts at offset `0x50`).
Write it to whatever stands in for the card, then follow steps 4–6 above. A Xenomorpher with firmware-card mode can serve it;
see the Xenomorphicle project.

## Selecting the Original tables
Power up **holding TIMBRE** until the LEDs come on, then release: Original, and remembered. Power up **holding SHAPE** the
same way: Twisted, and remembered. A normal power-up comes back in the mode you last chose (Twisted until you choose). See
[FIXED-BUGS.md](FIXED-BUGS.md).

## Verify your download
Compare the files with `SHA256SUMS`:
`shasum -a 256 -c SHA256SUMS`

## Going back
Reflash Buchla's own 259E 31.2 the same way (load its `.hex` on the card and power on holding Remote Enable), or 31.2C2 /
31.2C1. This build writes exactly the flash areas Buchla's update writes and leaves the preset bank alone, but take a BACKUP
of your presets first, as you would before any firmware change. The stored mode byte stays in the calibration area; the other
builds ignore it.
