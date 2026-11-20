# Fixed bugs — 257e 30.2C1 (relative to Buchla 30.2)

None of these has been exercised on hardware yet; see the [release notes](RELEASE-NOTES.md#test-status).

## 1. Bus SAVE and RECALL accepted any slot number
**Symptom.** The module has 30 preset slots, but a SAVE or RECALL arriving over the bus was acted on for any slot number up to 255.
A SAVE for a slot beyond the 30 wrote the current settings into memory outside the preset bank (for the highest numbers, beyond
the end of the module's memory altogether, which can stop the module). A RECALL for such a slot loaded whatever was there as the
live settings.
**Cause.** The slot number was used without a range check.
**Fix.** SAVE and RECALL for a slot beyond the 30 are ignored. Slots 1 to 30 behave exactly as before, including the recall of the
first preset at power-up and the panel's own save.

## 2. The reply after a preset load ended in an accidental byte
**Symptom.** After loading a preset the module sends a short reply on the bus. Its last byte was never set and carried whatever
value was left in memory, so it differed from one reply to the next.
**Cause.** A missing store when the reply is built. The same slip exists in the 251e's 30.7.
**Fix.** The last byte is now the module's own address, as in the community 251e builds.

## 3. A bus message could corrupt a queued panel or timer event
**Symptom.** Rarely, a button press, a pot event or a timer event could be lost or replaced by a stale one when a bus message
arrived at the same instant.
**Cause.** While an event was being added to the module's internal queue, bus reception was still allowed to add its own event to
the same queue, and the two could collide.
**Fix.** The queue is now protected against all interruptions for the few millionths of a second an add or a remove takes.

## Version
The module reports **30.2C1** in the version announcement it sends from the panel.
