# Known issues and behaviour that is unchanged from Buchla's 30.7

## Test status: what has and has not run on hardware
This is a pre-release (release candidate). Be clear about how little of it has been tried on a real module.

**Sequencer fixes (items 1–18 in [FIXED-BUGS.md](FIXED-BUGS.md)).** The 30.7C3 sequencer code was run on one module (loaded on
2026-10-23) in a build that did not yet contain the calibration code; the sequencer code in this image is byte-identical to it. Of the
11 checks on the bench checklist, **tests 1 and 2 passed** (the CV knob, and loop nesting, which played the expected order
`1 2 3 4 5 4 5 6 7 2 3 4 5 4 5 6 7 8`). **Tests 3 to 11 have not been run**: START clearing loop counters, the ghost loop, CV stage-select
hysteresis, the three pulse changes, tempo drift, the absolute tempo constant and SAVE without a pause. Those fixes are checked against
a model of the firmware only. A result on your module that differs from the one described is a finding worth reporting.

**The merged image (with the calibration code).** On 2026-10-26 this image was loaded onto a real 251e through the Xenomorpher card
route. After the load the module answers the calibration status request (it did not before), so the loader did program the extra
flash page. The status read "no valid record". Afterwards, three measuring-only calibration runs were made against the module from a
Xenomorpher, with writing disabled in the Xenomorpher: the module held its four CV outputs at set values, the Xenomorpher read them
back, and each run was discarded without writing. In the two logged runs the computed gains agreed within one step and the offsets exactly; the
first run was read from a screen photo and differed by three steps in the gain of one channel (cause not found). Separately, a held
output was released by itself after 5 seconds, and an explicit release returned the output within half a second.

**Nothing has ever been WRITTEN to a real unit with this firmware.** No calibration record has been stored on any module. The write
path (staging a record and committing it to flash) has been exercised only in an emulator and by code review. Playing with a stored
record, the corrected CV values, flash endurance of the record page, and whether a record survives a reflash are all untested.
Neither the presets nor normal sequencer playback were checked after this image was loaded; the two passed sequencer checks ran on the earlier build.

## Two different builds report 30.7C3
An earlier internal build, **without** the calibration code, reports the same version string `30.7C3`. It was never published. To tell
them apart:
- by the sha256 of the file you loaded: this image is `d4ed6432953203e39b50b6bebafce3121ab90e56b258984cccbadda0226f31f9` (hex) and
  `ac34bb71121fd9173c42e08b8f7abc6e8949c07e522f1140b0cdfb3d521b3ebd` (card image);
- by behaviour: only this image answers the calibration status request (command 0x18, "what" 2) on the bus; the other drops it.
The module's own version display cannot tell them apart. The card image's header carries no community version (only the module name).

## Calibration code: what to know
- Nothing uses it unless a Xenomorpher sends the calibration commands. A module with no stored record behaves like the sequencer-only
  build.
- The commands are plain bus frames with no protection against a deliberate sender: any device that sends a valid, correctly
  checksummed record for this module type to the module can store it. No public tool writes a record yet.
- The module pauses a few milliseconds while a record is saved; do this with the sequencers stopped.
- The extra flash page is described in [INSTALL.md](INSTALL.md#the-extra-flash-page).

## Bugs in Buchla's 30.7 that are NOT fixed here
These were found by testing the stock code and this image's code (they are the same code in both). Each was reproduced by running the
real bytes in a model of the processor, except the last, which was found by reading the code.
- **Sync-next ring.** If sync-next is set on stage 1 of all four sequencers (with no init delay), entering any of those stages starts
  a ring of sequencers starting each other that never returns; within a few milliseconds it overwrites the module's RAM and the
  module freezes until power is removed. Presets are not written by this. Do not set it. Do not SAVE a preset with this setting either: recalled with the sequencer running, it may freeze the module again (not tested).
- **Bus COPY and SWAP with a slot out of range.** Their slot numbers are not checked. A frame with an out-of-range slot, or a last
  slot of 255, can rewrite flash beyond the preset bank, **including the page that holds the calibration record**, or loop for ever
  rewriting flash. No known preset manager sends an out-of-range COPY or SWAP (the reference preset master sends neither); a hand-made frame can.
- **A short or empty bus frame repeats the previous command** with its previous arguments (for example a SAVE or RECALL again).
  A bus glitch or an aborted master can cause it.
- **A bus frame longer than 16 bytes wraps** around; its last bytes are read as a new command. No such frame is known today.
- **JA mode skips stage 1** when the jump pointer was left at stage 50.
- **RESTORE after a card read error still reports complete**, and recalls from a half-restored bank. (Found by reading the code, not
  by running it.)

## Not fixed in the sequencer, as in Buchla's 30.7 or 30.7C2
- The sync-next 1-tick lead (sync-next is only de-doubled, not aligned to the tick), the sample-and-hold stage-select offset of one
  stage ("1-46" report), the CV stage-select range at the top of the scale ("0-45" report), full-level "trans" for the whole pulse,
  the ¾ pulse width in bus-clock mode, the BACKUP missing pulses, RESTORE timing during card reads, and the preset manager's "not stored" LED
  for command 0x03 (by design).
- The flash-read erratum in SAVE.

## Assumptions not measured on a real module
- **The tempo constant (item 11)** is derived from the model: 125.00 ms per 1/16 at 120 BPM has not been measured on a module. If your
  scope shows otherwise, report the number.
- **SAVE without a pause (item 18)** assumes the processor's cycle counter keeps running while it waits for flash. If it does not,
  that item behaves like 30.7C2.
- **One knob step per click** is assumed, as in 30.7C2. If a knob on your unit steps two stages per click, go back to Buchla's 30.7
  and report it.

## Very fast turns
Each knob needs its contacts to hold still for about 2 ms before a step is counted. A flick faster than roughly 250 steps per
second on clean contacts, or 100–150 per second on worn ones, loses steps (Buchla's 30.7 stopped counting altogether above
about 200 per second). Contact flutter that lasts longer than the 2 ms settling time can still be read as a step in the wrong
direction, as on 30.7. These are limits of the knob, not of the sequencer.

## Remote Enable tap saves to preset 0
With no preset manager polling, tapping Remote Enable saves the current settings to preset slot 0 (documented in Buchla's 200e
guide). This is unchanged. All 30 presets live in one flash area, so a power loss during a SAVE can corrupt presets or make the
module reformat its bank. Keep a BACKUP of your presets.

## BACKUP while in Remote Enable
Buchla's note stands: take the 251e out of Remote Enable before a card BACKUP. With Remote Enable on, a BACKUP writes the module's
whole preset bank (about 63 KB) to the card from the starting address the manager supplies, which can overwrite other modules'
areas. Unchanged.

## Buttons share one debounce
All 21 buttons share one debounce state. Pressing a second button while the first is held can lose the first button's release
(modifier "held" states can stick; a Remote Enable hold may not be cancelled). Unchanged; only the sampling rate was changed.

## Waits on the bus
Several bus transfers still wait for the bus with no time limit, and the hardware watchdog remains off, as in 30.7. A stuck bus can
freeze the panel until power-cycle. Long operations (SAVE, BACKUP, RESTORE) can also drop panel events while they run.

## Version information
The module reports **30.7C3** (see above for the other build with the same string).

## Release candidate
This is a pre-release (release candidate 3). It replaces [30.7C2](../30.7C2/RELEASE-NOTES.md) as the newest build; 30.7C1 should no
longer be flashed.
