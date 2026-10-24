# Acoustic Sensor Driver (`firmware/drivers/microphone`)

**Status: Placeholder** - no driver code exists yet.

## Purpose

This directory will contain the integration of the acoustic sensing channel. Two options are under
consideration and the final choice is **planned**, not decided:

1. **Digital MEMS microphone** connected to the PDM interface of the nRF54LM20A, capturing airborne
   sound near the bearing.
2. **Piezoelectric contact sensor** mounted on the housing and sampled by the SAADC through a simple
   analog front end, capturing structure-borne acoustic emission.

The acoustic channel is intended to complement vibration by capturing higher-frequency friction,
lubrication deficiency, and early surface damage.

## Expected files

| File | Planned content |
|---|---|
| `acoustic.h` | Common API independent of the sensor type: `acoustic_init()`, `acoustic_start()`, `acoustic_stop()`, `acoustic_read_block()` |
| `acoustic_pdm.c` | PDM MEMS microphone backend using the Zephyr audio DMIC API (`dmic_configure`, `dmic_read`), block-based buffers |
| `acoustic_piezo_adc.c` | Piezo backend: SAADC sampling at a fixed rate via timer trigger and DMA, DC-offset handling |
| `acoustic_selftest.c` | Start-up checks: non-zero signal, absence of clipping, expected noise floor at standstill |
| `Kconfig` | Backend selection (`CONFIG_BGAI_ACOUSTIC_PDM` / `CONFIG_BGAI_ACOUSTIC_PIEZO`), sample rate, gain |
| `CMakeLists.txt` | Adds the selected backend to the build |

## Planned requirements

| Requirement | Preliminary target | Rationale |
|---|---|---|
| Sample rate | TODO (for example 16 kHz for PDM; piezo rate depends on analog front end) | Covers the audible band relevant to friction and impacts within RAM limits |
| Block size | Matched to the DSP window | Simplifies windowing |
| Dynamic range | Avoid clipping at Red-level fault severity on the rig | Needs measurement on the rig |
| Placement | Close to the test bearing, shielded from the motor and coupling | Reduce contamination by other noise sources |

## Privacy and data-retention note

An airborne microphone can capture speech in the laboratory. The planned design processes audio
**on the device** into energy and spectral features only; raw audio leaves the device solely in the
dedicated data-capture mode used during development, and raw recordings are not permanently retained
unless required and legally appropriate (see [`../../../datasets/README.md`](../../../datasets/README.md)).
A piezoelectric contact sensor largely avoids this concern and is a reason it remains a candidate.

## Planned implementation notes

- Both backends expose identical block-based output so the DSP module is independent of the choice.
- Gain and sample rate are compile-time options; runtime changes are not planned for the first version.
- Acoustic blocks are timestamped and aligned with vibration blocks for multisensor fusion.

## Current status

- Sensor type not yet selected; no code written.
- PDM and SAADC availability on the nRF54LM20 DK is to be confirmed in the pinned SDK release.

## TODO

- [ ] Compare a PDM MEMS microphone and a piezo contact sensor on the rig during the signal-analysis phase.
- [ ] Define the sample rate and block size together with the DSP design.
- [ ] If the piezo option is chosen, design and document the analog front end in `hardware/schematics/`.
- [ ] Implement the chosen backend and self-test.
