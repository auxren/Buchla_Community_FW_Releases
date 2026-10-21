# Fixed bugs and changes — 259e 31.2C2 (relative to Buchla 31.2)

## New in 31.2C2: Original wavetables at power-up
**What.** Hold the **TIMBRE** button while powering the system up, and keep holding it until the module's LEDs come on
(about a second). The module then runs with the a, b and c timbre positions pointing at the six factory transfer tables that
the Twisted firmware leaves unused: three per side, the tables of the original 259e Complex Waveform Generator. They are
ordered a, b, c on each side in the order they sit in the module's memory, which may not be the order the original panel
printed; listen and tell us.
**In that mode.** a, b and c behave like the numbered timbres: Warp folds the sine through the table, Morph crossfades, and
the FM knobs and inputs are FM (on Twisted they become table scanners for a, b and c). The memory-scan indication is off.
Timbres 1 to 5 are exactly as before.
**Back to Twisted.** Power up without holding TIMBRE. Holding the SHAPE button at power-up also selects Twisted, and
wins if both are held. The choice is not stored anywhere; every power-up decides again.
**Presets.** A preset only stores the timbre number. A preset saved on "a" plays the original table in Original mode and the
memory scan in Twisted mode. Nothing in the preset bank changes.
**The hold itself** is swallowed: holding TIMBRE at power-up does not step the timbre or switch the green/red side.

## 1. Panel freezes permanently if the bus master stops acknowledging while polling (from 31.2C1)
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

## 2. A knob edit could reach the sound engine half-updated (from 31.2C1)
**Symptom.** Very occasionally while turning a knob: a brief blip in pitch, warp or morph; or, after a long session, one
parameter sitting slightly away from where the knob and preset said it should be.
**Cause.** Knob values and parameters are two-byte quantities, written by the panel and read by the audio engine without
protection against the two sides interleaving. Because the knobs work relatively, a wrong knob reading was folded into the
parameter permanently.
**Fix.** The two accesses on the knob path are now indivisible.

## 3. A bus message could delay the audio engine (from 31.2C1)
**Symptom.** A faint crackle during bus traffic, if audible at all.
**Cause.** The bus interrupt had the same priority as the audio engine's sample interrupt.
**Fix.** The bus interrupt now runs below the audio interrupt. Bus timing is unaffected.

## 4. Short button taps were lost (from 31.2C1)
**Symptom.** A quick tap on Remote (or another button) sometimes did nothing.
**Cause.** The panel only sampled the buttons once every 42 ms.
**Fix.** Presses are now captured between samples, so every tap registers. Holds and long presses behave exactly as before.

## Version
The module reports **31.2C2** in the version announcement it sends from the panel.
