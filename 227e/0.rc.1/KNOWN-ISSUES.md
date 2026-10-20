# Known issues and behaviour that is unchanged from Buchla's 30.1

## Blips shorter than about 16 ms are ignored
The panel only looks at the buttons every 16 ms. A contact blip shorter than that is never seen. This is intended (it keeps noise out) and unchanged.

## Two buttons in the same instant
If two different buttons change within the same few milliseconds, only the later one registers. Unchanged from Buchla's 30.1.

## Bus waits have no time limit
Some bus transfers wait with no time limit, as in Buchla's 30.1; a fault on the bus can still hang the module until a power cycle.

## Timing figures are calculated, not measured
The tap timings above follow from the panel look interval (about 16 ms), which is derived from the module's clock setup, not measured on a module.

## Version information
The module reports **0.rc.1**. The firmware-card image header still reads 30.1 (cosmetic).

## Release candidate
This build has **not yet been run on a module**; it has only been checked in the lab. Everything above that is described as fixed is
unconfirmed on hardware until someone tries it.
