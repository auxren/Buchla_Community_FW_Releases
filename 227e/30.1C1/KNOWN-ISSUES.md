# Known issues and behaviour that is unchanged from Buchla's 30.1

## Blips shorter than about 11 ms are ignored
The panel only looks at the buttons every 10.7 ms. A contact blip shorter than that is never seen. This is intended (it keeps noise out) and unchanged.

## Two buttons in the same instant
If two different buttons change within the same few milliseconds, only the later one registers. Unchanged from Buchla's 30.1.

## Bus waits have no time limit
Some bus transfers wait with no time limit, as in Buchla's 30.1; a fault on the bus can still hang the module until a power cycle.

## Timing figures are calculated, not measured
The tap timings above follow from the panel look interval (10.7 ms), which is derived from the module's processor (a C8051F31x running at 24.5 MHz, accurate to about 2 %) as read from the firmware, not measured on a module.
An earlier version of these notes assumed a 16 MHz processor and quoted a 16 ms look interval and 33 ms / 50 ms tap limits; those figures were wrong and are corrected here.

## Switch bounce
Because a press now only needs to last about 11 ms to be possible, a panel switch that bounces for longer than about 10 ms could register twice. This has not been measured on a module. If a button double-triggers, please report which one.

## Version information
The module reports **30.1C1**. The firmware-card image header still reads 30.1 (cosmetic).

## Release candidate
This build has **not yet been run on a module**; it has only been checked in the lab. Everything above that is described as fixed is
unconfirmed on hardware until someone tries it.
