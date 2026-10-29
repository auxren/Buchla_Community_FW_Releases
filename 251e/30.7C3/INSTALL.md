# Installing 251e 30.7C3

**Before you start:** take a BACKUP of your presets (take the 251e out of Remote Enable first, see
[KNOWN-ISSUES.md](KNOWN-ISSUES.md)) and keep Buchla's own 251E 30.7 (from buchla.com) and, if you want the knob fixes only, the
earlier [30.7C2](../30.7C2/INSTALL.md) on hand so you can go back. This is a pre-release; flash it only on a module you can afford to
reflash. Do not flash while the 200e system is under power if your tool warns you not to.

**Never program the module's chip directly with a debug adapter** (a Silicon Labs USB Debug Adapter with SiUtil or the
Flash Programming Utility, an Atmel/Microchip JTAG tool, or any other JTAG/C2 programmer). Buchla locks the module's flash at the
factory; those tools can only get past the lock by erasing the whole chip, which destroys the module's bootloader, its factory
tables and calibration, and its presets. The files here are meant only for the firmware-card route or a device that stands in
for the card, as described below.

## With a device that stands in for the card (the route this image has been loaded by)
`251Ev307_30.7C3.card.bin` is the image laid out as a 224 KB firmware-card image of the larger layout used by the 200e's 32-bit
modules. It needs a card stand-in that supports that larger card (three-byte addressing), for example a Xenomorpher serving it as its
firmware card; the 64 KB stand-ins used for the 8-bit modules cannot serve it.
1. Power off the 200e system and put the card image on the stand-in following its own instructions.
2. Power on the system **while holding the 251e's Remote Enable button**; keep holding until the module's LEDs change and the
   loader has finished reading the card (with a Xenomorpher, until its bus counters stop moving).
3. Wait for the module to program itself, then power-cycle the system normally.
4. Check the module announces **30.7C3** (hold Remote Enable for about a second; with a preset manager attached the version appears
   on the bus). Because an earlier internal build reports the same string, also compare the sha256 of the file you loaded with
   `SHA256SUMS` (see [KNOWN-ISSUES.md](KNOWN-ISSUES.md#two-different-builds-report-307c3)).

While loading, keep other development modules that read the firmware card off the bus. On the one occasion this image was loaded,
two attempts stalled part-way and the third completed after another module that uses the card address was taken off the bus, the
card stand-in was restarted and Remote Enable was held throughout; which of the three mattered was not established.

## With Buchla's USB Firmware Card
`251Ev307_30.7C3.hex` can be given to Buchla's firmware utility like the earlier releases: load it onto the card, put the card in the
200e card slot, power on holding Remote Enable, wait one to two minutes, power-cycle. **This route has not been tried with this
image.** The image programs one flash page more than Buchla's own update does (see below), and it has not been confirmed that
Buchla's loader accepts that.

## The extra flash page
Buchla's update programs 112 flash pages. This image programs 113: the same 112 plus one page of previously unused space that holds the
calibration code. The preset bank and the page that holds a stored calibration record are not written by the update. The loader
programming the extra page was confirmed on one module through the card stand-in route (the module answered the calibration status
request after loading and did not before). Whether a stored calibration record survives a reflash has not been tested.

## Verify your download
Compare the files with `SHA256SUMS`:
`shasum -a 256 -c SHA256SUMS`

## Going back
- To Buchla's own 30.7: load its `.hex` the same way (on the card, power on holding Remote Enable). Take a BACKUP of your presets first,
  as you would before any firmware change.
- To the previous community build [30.7C2](../30.7C2/INSTALL.md): load its image the same way. 30.7C2 has no calibration code, so it
  ignores the calibration commands and does not apply a stored record. Whether a reflash keeps or erases a stored record has not been tested.
Check the version the module announces afterwards.
