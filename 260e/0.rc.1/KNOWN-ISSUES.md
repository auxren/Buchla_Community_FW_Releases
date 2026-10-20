# Known issues and behaviour that is unchanged from Buchla's 30.1

## A long press blocks the panel briefly
While the module is sending the message that a long press triggers, the display scan and button scan wait for it to finish
(about one to three and a half milliseconds on a healthy bus). This is Buchla's original behaviour and is unchanged; only the
unlimited wait is removed.

## Other bus waits are untouched
Only the two waits described under "Fixed bugs" are limited. The module has no hardware watchdog running, as in 30.1; a different
fault could still hang it until a power cycle.

## Timing figures are approximate
The time limits (about 0.1 s and about 0.04 s) follow from the instruction count and the module's clock setup, which was read from
the code and not measured on a module.

## Version information
The module reports **0.rc.1**. The firmware-card image header still reads 30.1 (cosmetic).

## Release candidate
This build has **not yet been run on a module**; it has only been checked in the lab. The fix is unconfirmed on hardware until someone
tries it, in particular with a deliberately stuck bus.
