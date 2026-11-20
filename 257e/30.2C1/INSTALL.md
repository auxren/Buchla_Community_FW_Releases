# Installing 257e 30.2C1

**Before you start:** check that your 257e reports **30.2** (hold Remote Enable for about two seconds with a preset manager in the
system); if it reports anything later, do not install. Take a BACKUP of your presets (installing erases them) and keep Buchla's own
257E 30.2 (from buchla.com) on hand so you can go back. This is a pre-release; flash it only on a module you can afford to reflash.

**Never program the module's chip directly with a debug adapter** (a Silicon Labs USB Debug Adapter with SiUtil or the
Flash Programming Utility, an Atmel/Microchip JTAG tool, or any other JTAG/C2 programmer). Buchla locks the module's flash at the
factory; those tools can only get past the lock by erasing the whole chip, which destroys the module's bootloader, its factory
tables and calibration, and its presets. The files here are meant only for the firmware-card route or a device that stands in
for the card, as described below.

## With a device that stands in for the card (the route this image has been loaded by)
`257Ev302_30.2C1.card.bin` is the image laid out as a 224 KB firmware-card image of the larger layout used by the 200e's 32-bit
modules. It needs a card stand-in that supports that larger card (three-byte addressing), for example a Xenomorpher serving it as its
firmware card; the 64 KB stand-ins used for the 8-bit modules cannot serve it.
1. Power off the 200e system and put the card image on the stand-in following its own instructions. The stand-in must be running
   and serving before the 257e powers up.
2. Power on the system **while holding the 257e's Remote Enable button**; keep holding until the loader has finished reading the
   card. The 257e reads the card once, in under a minute, and programs itself as it reads.
3. Power-cycle the system normally.
4. Check the module announces **30.2C1** (hold Remote Enable for about two seconds with a preset manager in the system).

## With Buchla's USB Firmware Card
`257Ev302_30.2C1.hex` can be given to Buchla's firmware utility: load it onto the card, put the card in the 200e card slot, power on
holding Remote Enable, wait about a minute, power-cycle. **This route has not been tried with this image.**

## What the image covers
- Buchla's own `257Ev302.hex` is unusual among the 32-bit modules' files: besides the application it contains 32 KB for the area in
  front of it, where the module's loader lives (zeros and a jump to the application). Whether the loader skips that part when it
  programs from a card is not known to us. This image therefore contains the application only, like Buchla's files for the other
  32-bit modules, and the module's loader area is not touched. The one load done so far confirms the loader accepts such an image.
- The image adds 24 bytes of code in previously unused space. They lie in a flash page that Buchla's update already programs, so no
  additional page is written.

## Verify your download
Compare the files with `SHA256SUMS`:
`shasum -a 256 -c SHA256SUMS`

## Going back
Reflash Buchla's own 257E 30.2 the same way. Note that Buchla's file includes the loader area described above; loading it from a
card has not been tried by us.
