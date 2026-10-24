# Data Collection Plan

**Status: Draft.** No data has been collected. This plan defines how recordings will be made so that
the resulting dataset supports honest training and evaluation of the anomaly model.

## 1. Objectives

1. Record a **healthy baseline** that covers the full planned range of speed and load for several
   bearing specimens.
2. Record **controlled deviation conditions** at multiple severities and speeds in independent runs.
3. Produce metadata that allows every result to be broken down by condition, severity, RPM, load, and
   bearing specimen.
4. Avoid data leakage by splitting datasets **by complete measurement run**.

## 2. Prerequisites

- Test rig built and safety-reviewed ([`test_rig_plan.md`](test_rig_plan.md), [`safety.md`](safety.md)).
- Firmware capture build streaming validated raw data ([`../firmware/README.md`](../firmware/README.md)).
- Capture tool writing files and metadata ([`../tools/data_capture/README.md`](../tools/data_capture/README.md)).
- Controlled vocabularies for conditions, severities, and positions defined
  ([`../datasets/metadata/README.md`](../datasets/metadata/README.md)).

## 3. Run structure

A **measurement run** is one continuous recording at one configuration (bearing, condition, severity,
load, speed set-point). Preliminary structure:

| Phase | Purpose | Duration (TODO) |
|---|---|---|
| Warm-up (not recorded or flagged) | Reach thermal and mechanical steady state after start | TODO |
| Steady-state recording | Main data | TODO (long enough for many analysis windows) |
| Optional ramp (flagged) | Speed sweep for RPM-dependence analysis | TODO |

Each run receives a unique `recording_id` and a metadata row. Runs are never merged.

## 4. Test matrix (preliminary)

| Dimension | Planned values |
|---|---|
| Bearing specimens | Several healthy specimens (`BRG01`...); several pre-worn specimens |
| Speed set-points | At least three speeds within the controlled range (values TODO) |
| Load levels | `L0` (none) plus at least two indexed settings (TODO) |
| Conditions | healthy_baseline, imbalance, misalignment, loose_mounting, increased_load, pre_worn_bearing |
| Severities | `none` for healthy; `s1`-`s3` per condition (definitions TODO in the test-rig risk assessment) |
| Repetitions | At least N independent runs per cell (N TODO), on different days where possible |

Not every combination needs to be recorded; the healthy baseline must cover all speeds and loads,
and each fault condition must be recorded at all speeds for at least one load.

## 5. Campaigns

| Campaign | Content | Milestone |
|---|---|---|
| C0 - Rig characterisation | Run-up/run-down sweeps with a healthy bearing to find rig resonances; tap tests on the structure | M4 |
| C1 - Healthy baseline | All speeds and loads, several specimens, several days | M4 |
| C2 - Imbalance | Severities s1-s3 at all speeds | M6 |
| C3 - Misalignment | Severities s1-s3 at all speeds | M6 |
| C4 - Loose mounting | Severities s1-s3 at all speeds (strict safety bounds) | M6 |
| C5 - Increased load | Load levels beyond baseline range at all speeds | M6 |
| C6 - Pre-worn bearings | Each specimen at all speeds and baseline loads | M6 |
| C7 - Healthy re-check | Healthy specimens again after fault campaigns to detect rig drift and remount effects | M6 |

## 6. Metadata

Every run records at minimum: `recording_id`, `bearing_id`, `timestamp`, `test_condition`,
`severity`, `rpm`, `load_level`, `accelerometer_position`, `acoustic_sensor_type`,
`acoustic_sensor_position`, `ambient_temperature_c`, `housing_temperature_c`, `sample_rate_hz`,
`window_duration_ms`, `operator_notes`, `dataset_split`. Template:
[`../datasets/metadata/recording_metadata_template.csv`](../datasets/metadata/recording_metadata_template.csv).

Operator notes must mention anything unusual (bench knocked, door slammed, speed instability) so that
runs can be excluded with a reason.

## 7. Dataset splits

- Partitioning is **by complete run**; windows from one run never appear in two partitions.
- Preferably, bearing specimens are also disjoint between train and test.
- Healthy runs are divided into train / validation / test; fault runs go to validation / test only
  (the anomaly model is trained on healthy data).
- `dataset_split` is assigned when the campaign is complete and then frozen; changes are logged.

## 8. Data handling and retention

- Raw data is stored in the external data directory, never in the repository.
- Raw audio is retained only if required and legally appropriate; the default is deletion after
  feature extraction and a short verification period (TODO: define period). Retention status is
  recorded in metadata.
- Any synthetic or augmented data is labelled `data_origin = synthetic | augmented`.
- Backups of the external store: TODO.

## 9. Quality criteria for a valid run

- Integrity report clean (no gaps, no saturation beyond a threshold, stable sample rate).
- RPM stable within a tolerance during the steady-state phase (tolerance TODO).
- Metadata complete and vocabulary-conformant.
- Pre-run checklist executed (safety).

## 10. Current status

- Plan only. No campaign has started.

## TODO

- [ ] Fix speeds, loads, severities, durations, and N with the rig design and risk assessment.
- [ ] Decide raw-audio retention period and document the legal basis for the recording location.
- [ ] Prepare run sheets / checklists for the operator.
