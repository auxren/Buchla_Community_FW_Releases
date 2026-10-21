# Fixed bugs — 272e 31.0C1 (relative to Buchla 31.0b1)

## 1. Display and LEDs freeze for about 2 seconds after turning a tuner knob quickly
**Symptom.** Turning a tuner's encoder several notches quickly froze every display and LED for roughly 1.6–2.2 s
(it scaled with the number of notches), and then everything caught up.
**Cause.** Each encoder notch queued a panel event, and the module drained the whole queue before refreshing the panel.
Every event retuned the FM tuner chip, which takes about 60 ms, so 30 notches meant about 2 s with no refresh.
**Fix.** While more panel events are waiting, the retune is deferred. When the queue is empty the module retunes once,
to the final frequency of each tuner. Nothing is retuned twice, and the radio always ends on the frequency shown.

## 2. Lag after pressing Remote or other panel controls
**Symptom.** The Remote LED, and other panel actions, followed the button press after a noticeable delay.
**Cause.** Every panel action sends a notification over the 200e bus, and the module waited for that transmission to finish
before carrying on.
**Fix.** The panel no longer waits for the bus message to complete.

## 3. Permanent lock-up if the 200e bus is slow, busy or stuck
**Symptom.** With a slow bus, a missing acknowledge or a bus held low, the module stopped responding until power-cycled.
**Cause.** The module waited for the bus at three points with no time limit.
**Fix.** Each of the three waits now gives up after about 10 ms and the module recovers, using Buchla's own abort routine
for a failed transmission.

## 4. A stray key code 23 halted the module
**Symptom.** Occasionally the module stopped responding permanently; only a power cycle recovered it.
**Cause.** Key code 23 from the panel scanner was handled as an endless loop.
**Fix.** Key code 23 is now ignored.

## 5. A stuck panel-encoder line could freeze the whole module
**Symptom.** If the panel encoder line stayed active, the module stopped doing anything else.
**Cause.** The panel interrupt waited for the encoder line to be released with no time limit, with other work blocked meanwhile.
**Fix.** The wait is limited to about 0.5 ms. If the line is still stuck, the panel interrupt is switched off and the module keeps
running, and it is switched on again automatically as soon as the line is idle.

## 6. A burst of panel events could wipe the whole event queue
**Symptom.** After a very fast burst of controls, the panel could ignore everything that had been queued.
**Cause.** The 128-byte panel event queue had no check for being full, so new events could overwrite unread ones and make the
queue look empty.
**Fix.** When the queue is full, new events are dropped instead (capacity 127 events); queued events are never lost.

## 7. Card BACKUP and RESTORE could hang the module
**Symptom.** A BACKUP or RESTORE with a wedged bus froze the module permanently.
**Cause.** Four places in the card routines waited for the bus to become idle with no time limit.
**Fix.** Each of the four waits now gives up after about 80 ms and the transfer continues, so a failure is reported through the
routine's normal status handling instead of freezing the module.
