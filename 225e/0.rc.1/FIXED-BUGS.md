# Fixed bugs — 225e 0.rc.1 (relative to Buchla 30.9)

## 1. Encoder clicks could be lost
**Symptom.** Occasionally a click of the encoder did nothing, more often on a worn encoder or when turning quickly.
**Cause.** When the encoder contacts chatter, an edge could arrive in the instant between the module reading the encoder pins and acknowledging the edge. The edge was acknowledged without ever being read, so the module lost track of the knob position and discarded the next click as well.
**Fix.** The module now makes sure a late edge is always noticed.

## 2. First click after power-up could restart the display
**Symptom.** If the first thing done after power-up was to turn the encoder (before any button press or bus message), the click was lost and the display went through its start-up again.
**Cause.** The page that should receive the click had not yet been selected, and the module jumped to nothing.
**Fix.** A click with no page selected yet is now simply dropped. As soon as any page is selected, the encoder works as before.

## Version
The module reports **0.rc.1** in its version announcement.
