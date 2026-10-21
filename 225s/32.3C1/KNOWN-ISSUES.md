# Known issues and behaviour that is unchanged from Buchla's 32.3

## Encoder is ignored during long operations
While the module is busy with a save, load or transfer, encoder clicks are deliberately discarded (not queued), and the position tracking can shift by one transition afterwards. This is Buchla's design and is unchanged.

## Brief blind spot when a message is shown
Each time the button-5 message is shown, the encoder is not watched for a few milliseconds. Unchanged.

## Direction page
On one display page the encoder only shows a direction indicator; any number of clicks fold into one. Unchanged.

## Clicks can fire mid-detent after a stray transition
After an odd number of transitions the click point shifts by half a detent until the next stray transition. This fix removes the usual cause, not the effect. Unchanged.

## Waits without a time limit
The LCD, UART and bus handling wait without a time limit; a failed LCD or bus can hang the module. Unchanged.

## Version information
The module reports **32.3C1**. The firmware-card image header still reads 32.3 (cosmetic).

## Release candidate
This build has **not yet been run on a module**; it has only been checked in the lab. Everything above that is described as fixed is
unconfirmed on hardware until someone tries it.
