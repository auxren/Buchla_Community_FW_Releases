# Buchla Community FW Releases

Community-maintained firmware builds for Buchla 200e modules. This repository holds **releases only**:
the firmware images, their checksums, and the documentation for each release.

| Module | Release | Based on | Status |
|---|---|---|---|
| 272e Polyphonic Tuner | [31.0C1](272e/31.0C1/RELEASE-NOTES.md) | Buchla 272E **31.0b1** | release candidate |
| 259e Twisted Waveform Generator | [31.2C2](259e/31.2C2/RELEASE-NOTES.md) (adds Original wavetables at power-up) | Buchla 259E **31.2** | release candidate; the new feature is **not yet run on hardware** ([31.2C1](259e/31.2C1/RELEASE-NOTES.md) remains available) |
| 210e Control & Signal Router | [30.5AC1](210e/30.5AC1/RELEASE-NOTES.md) | Buchla 210E **30.5A** | release candidate, **not yet run on hardware** |
| 225e MIDI Decoder / Preset Manager (225E MIDI processor) | [30.9C1](225e/30.9C1/RELEASE-NOTES.md) | Buchla 225E **30.9** | release candidate, **not yet run on hardware** |
| 225e MIDI Decoder / Preset Manager (225S storage processor) | [32.3C1](225s/32.3C1/RELEASE-NOTES.md) | Buchla 225S **32.3** | release candidate, **not yet run on hardware** |
| 226h Control Voltage Processor | [30.1C1](226h/30.1C1/RELEASE-NOTES.md) | Buchla 226H **30.1** | release candidate, **not yet run on hardware** |
| 227e System Interface | [30.1C1](227e/30.1C1/RELEASE-NOTES.md) | Buchla 227E **30.1** | release candidate, **not yet run on hardware** |
| 250e Dual Arbitrary Function Generator | [30.6C1](250e/30.6C1/RELEASE-NOTES.md) | Buchla 250E **30.6b1** | release candidate, **not yet run on hardware** |
| 251e Quad Sequential Voltage Source | [30.7C1](251e/30.7C1/RELEASE-NOTES.md) | Buchla 251E **30.7** | release candidate, **not yet run on hardware** |
| 252e Polyphonic Rhythm Generator | [30.2C1](252e/30.2C1/RELEASE-NOTES.md) | Buchla 252E **30.2** | release candidate, **not yet run on hardware** |
| 260e Duophonic Pitch Class Generator | [30.1C1](260e/30.1C1/RELEASE-NOTES.md) | Buchla 260E **30.1** | release candidate, **not yet run on hardware** |
| 291e Triple Morphing Filter | [30.1C1](291e/30.1C1/RELEASE-NOTES.md) | Buchla 291E **30.1** | release candidate, **not yet run on hardware** |

These are community builds provided **as is, without warranty**. They are not Buchla factory firmware.
Flashing firmware can leave a module unusable until it is reflashed; keep the base firmware for your module on hand
(each release's notes say which version it was built from and how to go back).

Release candidates marked **not yet run on hardware** have been checked only in the lab; they are published for owners who can test them and report back. Each release's notes say what to check.

Version numbers are Buchla's version followed by `C` (a community build made with Claude) and a revision number:
`30.7C1` is the first community revision built on Buchla 30.7. A module reports this string on the bus when the preset manager
asks for its version, so it always says what it is based on. (Releases before 2026-10-20 were numbered `0.rc.1` / `0.rc.2`;
the images are the same except for the version string.)

Each release folder contains `RELEASE-NOTES.md`, `FIXED-BUGS.md`, `KNOWN-ISSUES.md`, `INSTALL.md`, the images and a `SHA256SUMS` file.
