# Installing 210e 30.5AC1

**Before you start:** take a BACKUP of your presets if your system has any, and keep Buchla's own 30.5A (`210Ev305A_SSM.hex` from buchla.com) on hand so you can go back. Do not flash while the 200e system is under power if your tool warns you not to.

## With Buchla's USB Firmware Card (the standard route)
1. Power off the 200e system. Connect the USB Firmware Card to your computer.
2. In Buchla's firmware utility, load `210Ev305A_30.5AC1.hex` onto the card. The file name keeps Buchla's pattern so the utility reads
   the module and version from it. Wait for the card LED to finish.
3. Put the card in the 200e card slot.
4. Power on the system **while holding the module's firmware-load button (Remote Enable on most modules; check Buchla's instructions for yours)**; keep holding until the module's LEDs change.
5. Wait one to two minutes for the module to program itself, then power-cycle the system normally.
6. Check the module's version announcement on the bus reads **30.5AC1**.

## With a device that stands in for the card
`210Ev305A_30.5AC1.card.bin` is the same image laid out as a 64 KB firmware-card image (the card's data starts at offset `0x50`).
Write it to whatever stands in for the card, then follow steps 4–6 above.

## Verify your download
Compare the files with `SHA256SUMS`:
`shasum -a 256 -c SHA256SUMS`

## Going back
Reflash Buchla's own 30.5A the same way (load its `.hex` on the card and power on holding the same button).
This build writes exactly the flash areas Buchla's update writes.
