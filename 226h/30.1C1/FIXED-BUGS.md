# Fixed bugs — 226h 30.1C1 (relative to Buchla 30.1)

The fix has not been run on hardware yet; see the [release notes](RELEASE-NOTES.md#test-status).

## 1. Fast turns of the rotary encoder dropped nearly every step
**Symptom.** Turning the module's rotary encoder briskly made it stop counting: above roughly 150 steps per second most or all steps
after the first were lost until you paused (at 200 steps per second essentially nothing got through).
**Cause.** The module ignored any encoder movement within 3 ms of the previous one, and every ignored movement restarted that 3 ms
wait, so a steady fast turn never got through. In addition, movements of the encoder's second signal were also taken as
"new movements", which cancelled a step that was being measured, and a step that took more than five readings to settle was
silently abandoned.
**Fix.** The wait is now 1 ms, the encoder's second signal no longer triggers anything by itself (it is still read to work out the
direction), and a step now has ten readings to settle. On clean contacts every step is counted up to about 200 steps per second
and most steps up to about 300 steps per second. Normal turning (up to about 100 steps per second) behaves as before.

## Version
The module reports **30.1C1** in the version announcement it sends from the panel.
