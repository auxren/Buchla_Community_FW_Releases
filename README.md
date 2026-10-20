# Buchla Community FW Releases

Community-maintained firmware builds for Buchla 200e modules. This repository holds **releases only**:
the firmware images, their checksums, and the documentation for each release.

| Module | Release | Based on | Status |
|---|---|---|---|
| 272e Polyphonic Tuner | [0.rc.1](272e/0.rc.1/RELEASE-NOTES.md) | Buchla 272E **31.0b1** | release candidate |
| 259e Twisted Waveform Generator | [0.rc.2](259e/0.rc.2/RELEASE-NOTES.md) (adds Original wavetables at power-up) | Buchla 259E **31.2** | release candidate; the new feature is **not yet run on hardware** ([0.rc.1](259e/0.rc.1/RELEASE-NOTES.md) remains available) |
| 210e Control & Signal Router | [0.rc.1](210e/0.rc.1/RELEASE-NOTES.md) | Buchla 210E **30.5A** | release candidate, **not yet run on hardware** |
| 225e MIDI Decoder / Preset Manager (225E MIDI processor) | [0.rc.1](225e/0.rc.1/RELEASE-NOTES.md) | Buchla 225E **30.9** | release candidate, **not yet run on hardware** |
| 225e MIDI Decoder / Preset Manager (225S storage processor) | [0.rc.1](225s/0.rc.1/RELEASE-NOTES.md) | Buchla 225S **32.3** | release candidate, **not yet run on hardware** |
| 226h Control Voltage Processor | [0.rc.1](226h/0.rc.1/RELEASE-NOTES.md) | Buchla 226H **30.1** | release candidate, **not yet run on hardware** |
| 227e System Interface | [0.rc.1](227e/0.rc.1/RELEASE-NOTES.md) | Buchla 227E **30.1** | release candidate, **not yet run on hardware** |
| 250e Dual Arbitrary Function Generator | [0.rc.1](250e/0.rc.1/RELEASE-NOTES.md) | Buchla 250E **30.6b1** | release candidate, **not yet run on hardware** |
| 251e Quad Sequential Voltage Source | [0.rc.1](251e/0.rc.1/RELEASE-NOTES.md) | Buchla 251E **30.7** | release candidate, **not yet run on hardware** |
| 252e Polyphonic Rhythm Generator | [0.rc.1](252e/0.rc.1/RELEASE-NOTES.md) | Buchla 252E **30.2** | release candidate, **not yet run on hardware** |
| 260e Duophonic Pitch Class Generator | [0.rc.1](260e/0.rc.1/RELEASE-NOTES.md) | Buchla 260E **30.1** | release candidate, **not yet run on hardware** |
| 291e Triple Morphing Filter | [0.rc.1](291e/0.rc.1/RELEASE-NOTES.md) | Buchla 291E **30.1** | release candidate, **not yet run on hardware** |

These are community builds provided **as is, without warranty**. They are not Buchla factory firmware.
Flashing firmware can leave a module unusable until it is reflashed; keep the base firmware for your module on hand
(each release's notes say which version it was built from and how to go back).

Release candidates marked **not yet run on hardware** have been checked only in the lab; they are published for owners who can test them and report back. Each release's notes say what to check.

Each release folder contains `RELEASE-NOTES.md`, `FIXED-BUGS.md`, `KNOWN-ISSUES.md`, `INSTALL.md`, the images and a `SHA256SUMS` file.
