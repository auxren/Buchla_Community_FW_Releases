# Fixed bugs — 260e 30.1C1 (relative to Buchla 30.1)

## 1. The module can freeze permanently if the bus gets stuck while it sends a message
**Symptom.** If a long press of the panel button that makes the module send a message on the 200e bus coincided with a fault on the
bus (a line held low by a faulty or disconnected device, a hung neighbour), the module stopped responding: display, buttons and
everything else on the panel. Only a power cycle brought it back.
**Cause.** The module sends that message from inside a part of its program that also runs the display and the button scanning, and
then waits for the bus hardware to report the message finished, with no time limit. A message that never finishes therefore stops
everything. The same unlimited wait was used when the module waits for the bus to become free before it starts a message.
**Fix.** Both waits now have a time limit. If the bus does not finish the message within about a tenth of a second, the module abandons
it, records it as failed to send (the same record it makes when a receiver does not answer) and carries on; the panel works again at
once. When it waits for a busy bus before starting a message, it gives up after a few hundredths of a second and starts the message
anyway, as the bus hardware itself waits for the bus to be free. When the bus recovers, messaging works again without a power cycle.
A message on a healthy bus is not delayed.

## Version
The module reports **30.1C1** in the version announcement it sends on the bus.
