# Known issues and behaviour that is unchanged from Buchla's 30.1

## Do not install over 30.2
Some 267e modules carry firmware 30.2, which Buchla has not published and which we do not have. This build is based on 30.1 and
replaces whatever is on the module. If your module reports 30.2, keep it. The one module this build has been loaded on reported
30.2 beforehand; that firmware could not be read out first and is gone from that module.

## Checked on one module only
This build has been loaded and checked on one module. A long soak has not been done.

## The two mix pots at power-up and after a recall
These now follow the stored preset (see [FIXED-BUGS.md](FIXED-BUGS.md)). At power-up, and after any recall, the pot position on the
panel can differ from the mix in use until the pot is turned. This is how the module's other eight pots already behaved.

## Installing erases the presets
The update contains an empty preset bank, as Buchla's own does. Take a BACKUP first if the presets matter.

## Buttons
The buttons share one debounce state and a lockout of about a tenth of a second: a second button pressed shortly after the first can
be ignored. Unchanged.

## Timing runs about 9 % fast
The module's internal time base is about 9 % faster than nominal, so its button hold times are that much shorter than intended
(the 1.5 s hold is about 1.36 s). Unchanged.

## Waits on the bus
Some bus transfers wait with no time limit and the hardware watchdog remains off, as in 30.1. A stuck bus can freeze the module until
power-cycle. The module's event queue can also silently drop events if the main program stalls. A bus frame arriving at the wrong
moment can corrupt a panel event that is being queued. Unchanged.

## Preset slots are not range-checked
A RECALL sent over the bus for a slot beyond the 30 the module has is still acted on and loads meaningless values. Unchanged; preset
managers do not send such slots.

## Version information
The module reports **30.1C1**. The firmware-card image header still reads 30.1 (cosmetic). The module only announces its version
when a preset manager has polled the bus since power-up.

## Release candidate
This is release candidate 1.
