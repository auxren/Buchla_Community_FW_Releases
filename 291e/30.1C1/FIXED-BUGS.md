# Fixed bugs — 291e 30.1C1 (relative to Buchla 30.1)

## 1. One key code stops the module permanently
**Symptom.** If the key scanner ever reported key number 19, the module stopped dead: display, keys, sound control, everything, until a power cycle.
**Cause.** The handler for that key code ended in an endless loop.
**Fix.** That code now falls through to the normal end of the key handler, like an unused key.

## 2. A key line that stays active hangs the module
**Symptom.** If the key scanner chip held its data line for longer than expected (a stuck key, a slow release, a chip fault, a noisy line), the module froze.
**Cause.** After reading a key the module waited for the scanner to release its line, with no time limit, from inside a part of the program that blocks everything else.
**Fix.** The wait is limited to about half a millisecond. If the line is still active after that, key reading is switched off and is switched back on
automatically as soon as the line is seen released again. Normal key use is unchanged.

## 3. The key buffer could erase itself
**Symptom.** If keys arrived and were not read for a long time, the 128th unread key press made the module forget all 128 of them.
**Cause.** The buffer had no check for being full: the write position caught up with the read position and the buffer then looked empty.
**Fix.** When the buffer is full the new key press is dropped and the buffer keeps what it has.

## 4. A display that does not answer hangs the module
**Symptom.** With the LCD missing, faulty or held busy, the module froze completely, including the parts of it that normally keep running in the background.
**Cause.** Before every character the module waits for the display to report ready, with no time limit.
**Fix.** The wait is limited to about 3 milliseconds (longer than the display's slowest command). If the display is not ready by then the module goes on; with a faulty
display a character may come out garbled instead of the module hanging.

## 5. A stuck bus hangs the module
**Symptom.** If the 200e bus stayed busy (a line held low), the module froze at its next bus message.
**Cause.** Several places waited for the bus to be free with no time limit.
**Fix.** Each such wait is limited to about 15 milliseconds; the module then goes on and starts its message, as the bus hardware itself waits for the bus to be free.

## Version
The module reports **30.1C1** in the version announcement it sends on the bus.
