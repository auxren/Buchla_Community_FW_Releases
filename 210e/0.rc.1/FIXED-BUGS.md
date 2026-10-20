# Fixed bugs — 210e 0.rc.1 (relative to Buchla 30.5A)

## 1. Rotary encoders skip steps, and sometimes step backwards
**Symptom.** Turning an encoder at more than a slow pace could make it miss detents. Now and then a turn in one direction
produced a step in the other direction. The faster the turn, and the more the module was busy (display updates, bus
traffic), the more steps were lost.
**Cause.** An encoder makes two contact changes for each detent, usually a millisecond or less apart. The module was deaf to its
encoders for roughly half of every internal update cycle (a few milliseconds each), and for a while after every encoder step
while it redrew the display. Two changes that both fell inside a deaf period were seen as a single jump, which the module
discards; three were seen as one step backwards.
**Fix.** The module now listens to its encoders all the time. The listener only counts what it sees; the counted steps are then
applied by the module's main program on its next pass, and the display is redrawn there too, not while listening.
Step size, the one-step-per-detent behaviour, display and bus behaviour are unchanged.

**One change in feel.** A turn is now applied on the module's next pass through its main program rather than at the very
instant it happens. That is a few milliseconds (up to about 5 ms) and is not expected to be noticeable. A step forward and a step back that
arrive within the same few milliseconds cancel out instead of both being applied.

## Version
The module reports **0.rc.1** in the version announcement it sends on the bus.
