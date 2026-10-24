# Project Log 01 - Concept, Planning, and Repository Scaffold

**Status: Draft for publication.** Date: TODO (set at publication).

## Summary

BearingGuard AI starts as a plan, not a prototype. This first log records what has been decided at the
concept stage, what the repository now contains, and what happens next. No hardware has been assembled,
no data has been recorded, no firmware runs, and no model has been trained.

## What was done

- Defined the project objective: early detection of deviation from a learned healthy bearing condition
  using three-axis vibration, acoustic, housing-temperature, and RPM sensing, with Edge AI on the Nordic
  nRF54LM20 DK and Bluetooth LE reporting.
- Chose the first realistic goal: **anomaly detection relative to a healthy baseline** on a controlled
  test rig - explicitly not fault classification or remaining-useful-life prediction.
- Drafted the preliminary system architecture in five layers (mechanical rig, sensing hardware,
  firmware, data and model pipeline, user interface).
- Defined the planned Edge AI processing flow and candidate features.
- Drafted the preliminary Bearing Health Service with twelve planned characteristics (UUIDs not yet allocated).
- Defined the test-rig concept with mandatory guard, independent emergency stop, and controlled maximum speed.
- Wrote the data-collection policy: run-level dataset splits, mandatory metadata, no large raw data in
  git, raw-audio retention limits, labelling of synthetic data.
- Created the preliminary bill of materials (all items planned, no part numbers).
- Created the model card placeholder, marked "not yet trained".
- Set up the public repository scaffold with placeholder READMEs explaining every planned directory.

## Decisions taken

| Topic | Decision |
|---|---|
| Platform | Nordic nRF54LM20 DK with nRF Connect SDK (Zephyr) |
| First objective | Anomaly detection vs. healthy baseline |
| Modelling | Stage 1 statistical detector; Stage 2 optional neural model |
| Data handling | Run-level splits; external storage for raw data |
| Safety | Guard and e-stop mandatory; device never controls the motor |
| License | Apache-2.0 |

## Open questions

- Acoustic sensor: MEMS microphone (PDM) or piezo contact sensor?
- Temperature sensing: digital sensors or NTC thermistors?
- Bearing size and drive-train dimensions.
- SDK release with nRF54LM20 DK support to pin.
- Inference runtime (TensorFlow Lite Micro, Edge Impulse, or statistical only).

## Next steps

1. Acquire the nRF54LM20 DK, sensors, and rig components (M1).
2. Write the risk assessment and design the guard; build the rig (M2).
3. Pin the SDK, verify the board target, and bring up sensor drivers (M3).

## Honest status line

Concept and planning stage. Nothing has been measured yet.
