# Fixed bugs — 250e 0.rc.1 (relative to Buchla 30.6b1)

## 1. Fast encoder turns skip steps or go the wrong way
**Symptom.** Turning the encoder briskly lost steps: a quick flick that should move the stage cursor (or change a value) by
eight or sixteen steps moved it by noticeably fewer, and a very fast spin could move it backwards. Slow, deliberate turns
were fine. Buchla's 30.5 behaves the same way, so this is not new in 30.6b1.
**Cause.** The module looks at the encoder only a few hundred times a second (about every 5 ms). If the knob moves two or
more positions between two looks, the module cannot tell which way it went, so it drops those steps; three positions at once
look like one step the other way. This starts to show above roughly 190 encoder positions per second and gets steadily worse.
**Fix.** The encoder is now looked at much more often: first twice as often as before, and in addition on the module's fast
2 kHz timer, so about every 0.5 ms. Lab checks show every step delivered, in both directions, at speeds up to about
1,900 encoder positions per second, well beyond what a hand can do. The CPU cost is well under 1 %. The slow-turn feel, the
step size (one step per detent) and the button handling are unchanged.

## Version
The module reports **0.rc.1** in the version announcement it sends from the panel.
