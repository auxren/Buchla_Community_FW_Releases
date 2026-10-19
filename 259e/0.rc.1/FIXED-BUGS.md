# Fixed bugs — 259e 0.rc.1 (relative to Buchla 31.2)

## 1. Panel freezes permanently if the bus master stops acknowledging while polling
**Symptom.** With the module in polling mode (a preset manager had started polling), unplugging or resetting the manager
and then touching a knob or button could leave the module with dead knobs, dead buttons and no response to bus commands.
The sound kept playing. Only a power cycle recovered it.
**Cause.** Every knob or button edit in polling mode sends a short reply on the bus. If nobody acknowledges that reply, the
module retried it forever and waited for it to finish with no time limit. The same unlimited wait was used before every bus
transmission and in the panel's bus re-initialisation.
**Fix.** A reply that is not acknowledged is now dropped, and repeated loss of the bus to another master gives up after a
generous number of attempts. Every wait on the bus is limited to about one second; on timeout the module resets its bus
interface, as it already does for an unknown bus state, reports the failure through the normal status path, and carries on.
When the master returns, the bus works again without a power cycle.

## 2. A knob edit could reach the sound engine half-updated
**Symptom.** Very occasionally while turning a knob: a brief blip in pitch, warp or morph; or, after a long session, one
parameter sitting slightly away from where the knob and preset said it should be.
**Cause.** Knob values and parameters are two-byte quantities. They were written by the panel and read by the audio engine,
and read from the converters, without protection against the two sides interleaving, so one side could occasionally see a
value made of one old byte and one new byte. Because the knobs work relatively (they move the parameter by how far the knob
moved), a wrong knob reading was folded into the parameter permanently. Buchla's 31.2 protected one such case (pitch set over
the bus) but not the knob path.
**Fix.** The two accesses on the knob path are now indivisible.

## 3. A bus message could delay the audio engine
**Symptom.** A faint crackle during bus traffic (for example while a preset manager polls), if audible at all.
**Cause.** The bus interrupt had the same priority as the audio engine's sample interrupt, so a bus byte arriving just before
a sample was due could push the longest sample computation past the sample period; the output then repeated one sample.
**Fix.** The bus interrupt now runs below the audio interrupt. Bus timing is unaffected: the bus hardware holds the clock
until the module is ready, and the extra delay is a few microseconds.

## 4. Short button taps were lost
**Symptom.** A quick tap on Remote (or another button) sometimes did nothing; it had to be pressed more deliberately. This is
the behaviour some owners described as "switching to remote takes a little patience".
**Cause.** The panel only sampled the buttons once every 42 ms, and a press that fell entirely between two samples was never
seen.
**Fix.** Presses are now captured between samples, so every tap registers. Holds and long presses behave exactly as before.

## Version
The module reports **0.rc.1** in the version announcement it sends from the panel.
