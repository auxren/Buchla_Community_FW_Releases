# Fixed bugs — 252e 30.2C1 (relative to Buchla 30.2)

Neither fix has been run on hardware yet; see the [release notes](RELEASE-NOTES.md#test-status).

## 1. Fast knob turns produce no steps
**Symptom.** Turning a panel knob quickly made it stop responding: above roughly 100 steps per second (a brisk turn) the steps
dropped to almost nothing until you paused. Turning two knobs together lost steps even at moderate speed.
**Cause.** After each knob movement the module ignored all knob movement, from any knob, for about 10 ms, and each ignored movement
restarted that 10 ms wait, so a steady fast turn never got through.
**Fix.** The wait is now about 7 ms and is counted from the last movement that was actually accepted, so it no longer extends
itself. A fast turn now produces a steady stream of steps instead of silence; two knobs together lose fewer steps than before.
Slow and moderate turning (up to about 100 steps per second) behaves exactly as before.
This improves the problem but does not remove it: see [KNOWN-ISSUES.md](KNOWN-ISSUES.md).

## 2. A second tap on a protected button within 0.2 s was ignored
**Symptom.** On the six buttons with built-in lockout (including the two knob push switches), a quick second tap or double-click
did nothing; tapping a different one of the six shortly after the first also failed.
**Cause.** A single 0.2-second lockout, shared by those six buttons, followed every accepted press.
**Fix.** The lockout is now about 40 ms. The contact-bounce filtering of those buttons is unchanged.

## Version
The module reports **30.2C1** in the version announcement it sends from the panel.
