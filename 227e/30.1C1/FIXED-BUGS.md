# Fixed bugs — 227e 30.1C1 (relative to Buchla 30.1)

## 1. Quick button taps were not registered
**Symptom.** A fast tap on a panel button sometimes did nothing. Taps shorter than about 1/30 s (33 ms) were never registered, and taps up to about 1/20 s (50 ms) registered only some of the time.
**Cause.** The panel looks at its buttons about 60 times a second and only believed a change after seeing the same reading on three looks in a row, so a press had to span at least two, and for certainty three, looks.
**Fix.** The panel now believes a change after two looks in a row. A press of about 1/30 s or longer always registers; a press between about 1/60 s and 1/30 s registers some of the time; a blip shorter than a single look (about 16 ms) is still ignored, as before.
**Side effect.** A button that acts when it is *released* now acts one look (about 16 ms) sooner. Holds, long presses and timeouts are unchanged.

## Version
The module reports **30.1C1** in its version announcement.
