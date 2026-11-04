# Fixed bugs — 227e 30.1C1 (relative to Buchla 30.1)

## 1. Quick button taps were not registered
**Symptom.** A fast tap on a panel button sometimes did nothing. Taps shorter than about 21 ms were never registered, and taps up to about 32 ms registered only some of the time.
**Cause.** The panel looks at its buttons about 93 times a second (every 10.7 ms) and only believed a change after seeing the same reading on three looks in a row, so a press had to span at least two, and for certainty three, looks.
**Fix.** The panel now believes a change after two looks in a row. A press of about 21 ms or longer always registers; a press between about 11 ms and 21 ms registers some of the time; a blip shorter than a single look (about 11 ms) is still ignored, as before.
**Side effect.** A button that acts when it is *released* now acts one look (about 11 ms) sooner. Holds, long presses and timeouts are unchanged.

## Version
The module reports **30.1C1** in its version announcement.
