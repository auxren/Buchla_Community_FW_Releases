# Known issues and behaviour that is unchanged from Buchla's 30.1

## Key responsiveness
Key presses can still wait a short time (up to a bit over half a millisecond, longer while the display is being updated) before they are read. This is
unchanged. Only hangs are fixed, not response time.

## Other waits are untouched
Only the waits listed under "Fixed bugs" are limited. Some other bus waits, and the hardware watchdog (still off), are as in Buchla's 30.1.

## Timing figures are approximate
The time limits follow from the instruction count and the module's clock setup, which was read from the code and not measured on a module.

## A full key buffer drops new keys
When the buffer is full, further key presses are lost until the module reads some. This replaces the old behaviour, where everything was lost at once.

## Version information
The module reports **30.1C1**. The firmware-card image header still reads 30.1 (cosmetic).

## Release candidate
This build has **not yet been run on a module**; it has only been checked in the lab. Everything described as fixed is unconfirmed on
hardware until someone tries it.
