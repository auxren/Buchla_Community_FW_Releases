# 226h Control Voltage Processor — Community firmware 30.1C1 (release candidate 1)

**Based on:** Buchla 226H firmware **30.1** (`226Hv301.hex`, Buchla download dated 2019-06-04, sha256
`4944b09e5dda909ead7d4f45b5d4b04c1571d4680d8a82bcf71b99671a2c01b6`).
Everything not listed under [Fixed bugs](FIXED-BUGS.md) is byte-for-byte Buchla's 30.1. The version this build reports
(the panel's version announcement on the bus) is **30.1C1**; the number is Buchla's version followed by `C` (a community build made with Claude) and a revision number, so the module always says what it is based on.

**Status: release candidate, not yet run on hardware.** See [Test status](#test-status).

## Files
| file | what | sha256 |
|---|---|---|
| `226Hv301_30.1C1.hex` | firmware image (Intel HEX) | `a987a30b6e399a453e3582ca074921536a55396ca7875abbf4b0b409a83ba25c` |
| `226Hv301_30.1C1.card.bin` | the same image as a 224 KB firmware-card image (the larger card layout used by the 200e's 32-bit modules) | `e5e3aab243d60b1225db835076688905b9e52ebb06b0fdf53d70b42bcc8db5af` |

The file names keep Buchla's `226Hv301…` naming pattern because Buchla's flashing tools read the module and version from it,
so the card image's header still shows version 30.1; that is cosmetic. The module itself reports 30.1C1.

The image occupies exactly the same flash areas as Buchla's own 30.1 update.

## What changed (summary)
One problem in 30.1 is improved, with a very small change. Details in [FIXED-BUGS.md](FIXED-BUGS.md).
1. Turning the module's rotary encoder quickly dropped nearly every step after the first; it now keeps counting steps up to
   roughly 200 steps per second on clean contacts. Extremely fast flicks can still be misread (see [KNOWN-ISSUES.md](KNOWN-ISSUES.md)).

Everything else, including the buttons, the bus behaviour and the presets, is unchanged.

## Test status
**Not yet run on hardware. Checked in the lab only.** No module has been flashed with this image. The behaviour of the rotary
encoder at normal and fast speed on a real 226h has not been tried; neither has a long soak. Reports are welcome.

## Installing and going back
See [INSTALL.md](INSTALL.md). To return to stock, reflash Buchla's own 30.1 the same way.
