# Installing 272e 0.rc.1

**Before you start:** keep Buchla's own 31.0b1 (or the version you run today) on hand so you can go back. Do not flash while the
200e system is under power if your tool warns you not to.

## With Buchla's USB Firmware Card (the standard route)
1. Power off the 200e system. Connect the USB Firmware Card to your computer.
2. In Buchla's firmware utility, load `272Ev310b1_0.rc.1.hex` onto the card. The file name keeps Buchla's pattern so the utility reads
   the module and version from it. Wait for the card LED to finish.
3. Put the card in the 200e card slot.
4. Power on the system **while holding the 272e's Remote button**.
5. Wait one to two minutes for the module to program itself, then power-cycle the system normally.
6. Check the module announces **0.rc.1** (key code 22 shows the version on the bus).

## With a device that stands in for the card
`272Ev310b1_0.rc.1.card.bin` is the same image laid out as a 64 KB firmware-card image (the card's data starts at offset `0x50`).
Write it to whatever stands in for the card, then follow steps 4–6 above.

## Verify your download
Compare the files with `SHA256SUMS`:
`shasum -a 256 -c SHA256SUMS`

## Going back
Reflash Buchla's own 272E 31.0b1 the same way (load its `.hex` on the card and power on holding Remote).
This build makes no changes to the module's preset flash page, but take a BACKUP of your presets first, as you would before any
firmware change.
