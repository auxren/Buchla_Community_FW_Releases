# Known issues and behaviour that is unchanged from Buchla's 30.1

## Not yet run on hardware
This candidate has been checked in the lab only and has never run on a module. Items listed under "Not yet run on hardware" in
the [release notes](RELEASE-NOTES.md) are still to be completed.

## Wrong-direction steps on very fast flicks
The encoder's direction is worked out from where its two signals settle after a movement. On a very fast flick, or when the second
signal follows the first very closely, that can come out reversed. This was already so in 30.1 and is not changed. Contact bounce at
around 100 steps per second can swap some lost steps for some wrong-direction steps; at normal speed this does not happen.

## What was assumed about the encoder
The behaviour was worked out from the firmware alone; the encoder itself has not been measured. If your unit counts a different
number of steps per click than before, please go back to Buchla's 30.1 and report it.

## Buttons
The buttons share one debounce state and a long lockout: a second button pressed shortly after the first can be ignored. Unchanged.

## Waits on the bus
Some bus transfers wait with no time limit and the hardware watchdog remains off, as in 30.1. A stuck bus can freeze the module until
power-cycle. The module's event queue can also silently drop events if the main program stalls for more than about 30 ms. Unchanged.

## Version information
The module reports **0.rc.1**. The firmware-card image header still reads 30.1 (cosmetic).

## Release candidate
This is release candidate 1.
