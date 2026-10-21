# Installing 226h 30.1C1

**Before you start:** keep Buchla's own 226H 30.1 (from buchla.com) on hand so you can go back. This candidate has not run on
hardware yet; flash it only on a module you can afford to reflash. Do not flash while the 200e system is under power if your tool
warns you not to.

## With Buchla's USB Firmware Card (the standard route)
1. Power off the 200e system. Connect the USB Firmware Card to your computer.
2. In Buchla's firmware utility, load `226Hv301_30.1C1.hex` onto the card. The file name keeps Buchla's pattern so the utility reads
   the module and version from it. Wait for the card LED to finish.
3. Put the card in the 200e card slot.
4. Power on the system **while holding the 226h's firmware-load button** (Remote Enable on most modules; follow Buchla's instructions for
   your module); keep holding until the module's LEDs change.
5. Wait one to two minutes for the module to program itself, then power-cycle the system normally.
6. Check the module announces **30.1C1** (with a preset manager attached, the version appears on the bus).

## With a device that stands in for the card
`226Hv301_30.1C1.card.bin` is the same image laid out as a 224 KB firmware-card image of the larger layout used by the 200e's 32-bit
modules. It needs a card stand-in that supports that larger card (three-byte addressing); the 64 KB stand-ins used for the 8-bit
modules cannot serve it. Write it to the stand-in, then follow steps 4–6 above.

## Verify your download
Compare the files with `SHA256SUMS`:
`shasum -a 256 -c SHA256SUMS`

## Going back
Reflash Buchla's own 226H 30.1 the same way (load its `.hex` on the card and power on holding the same button).
This build writes exactly the flash areas Buchla's update writes, but take a BACKUP of any presets first, as you would before any
firmware change.
