# Known issues and behaviour that is unchanged from Buchla's 30.2

## The fixes have not been exercised on hardware
The build loads, the module runs and reports the new version. The three fixes were checked in the lab only.

## Installing erases the presets
The update contains an empty preset bank, as Buchla's own does. Take a BACKUP first if the presets matter.

## A freeze after a bus SAVE has been seen, cause not established
On one occasion a 257e running Buchla's 30.2 froze after a SAVE sent to all modules over the bus. This build does not claim to fix
that: the likeliest cause is the unlimited bus waits described below, which are unchanged.

## Waits on the bus
Some bus transfers wait with no time limit and the hardware watchdog remains off, as in 30.2. A stuck bus can freeze the module until
power-cycle. The module also queues one event every thousandth of a second and handles one per pass of its main program, so a stall
of about 30 ms makes it drop events silently. Unchanged.

## Buttons
The buttons share one debounce state and a lockout of about a tenth of a second: a second button pressed shortly after the first can
be ignored. Unchanged.

## Pots at power-up
The module starts from its first preset, not from the panel; a pot takes effect once it has been turned. Unchanged.

## Remote Enable with no preset manager
With no preset manager having polled the bus since power-up, a short press of Remote Enable stores the current settings into the
first preset. Unchanged. The module also only announces its version (on a hold of about a second) once a preset manager has polled.

## Version information
The module reports **30.2C1**. The firmware-card image header still reads 30.2 (cosmetic).

## Release candidate
This is release candidate 1.
