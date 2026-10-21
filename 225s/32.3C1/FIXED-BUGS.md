# Fixed bugs — 225s 32.3C1 (relative to Buchla 32.3)

## 1. Encoder clicks could be lost
**Symptom.** Occasionally a click of the encoder did nothing, more often on a worn encoder or when turning quickly.
**Cause.** When the encoder contacts chatter, an edge could arrive in the instant between the module reading the encoder pins and acknowledging the edge. The edge was acknowledged without ever being read, so the module lost track of the knob position and the next click was misread as a double step and dropped.
**Fix.** The module now makes sure a late edge is always noticed.

## Version
The module reports **32.3C1** in its version announcement.
