# Known issues and behaviour that is unchanged from Buchla's 30.5A

## Buttons: two presses close together
A second button pressed within about 11 ms of the first can erase the first press, and two button events inside the same pass of the
main program can overwrite each other. This is Buchla's original behaviour and is unchanged.

## Bus waits have no time limit
Some waits on the bus have no time limit, as in Buchla's 30.5A; a fault on the bus can still hang the module until a power cycle.

## Display must be watched
The display is now redrawn from the main program instead of while the module is listening to the encoders. We have not yet seen
this on a module: the displays should never glitch while an encoder is turned quickly during bus traffic. A glitch would be worth reporting.

## Timing figures are calculated, not measured
The lost-step windows quoted for 30.5A (a few milliseconds blind in each update cycle) are derived from the code and the clock setup,
not measured on a module.

## Version information
The module reports **30.5AC1**. The firmware-card image header still reads 30.5A (cosmetic).

## Release candidate
This build has **not yet been run on a module**; it has only been checked in the lab. Everything described as fixed is unconfirmed on
hardware until someone tries it.
