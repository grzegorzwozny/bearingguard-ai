# Datasets

**Status: Planned** - no data has been recorded. This directory defines the dataset policy and holds
only documentation and templates.

## Purpose

BearingGuard AI will produce recordings of vibration, acoustic, temperature, and RPM signals from the
test rig under healthy and controlled fault conditions. This directory defines how those recordings are
organised, named, described, split, and stored, so that models trained from them are reproducible and
their evaluation is trustworthy.

## Directory overview

| Directory | Content | Status |
|---|---|---|
| [`raw/`](raw/README.md) | Placeholder for raw recordings; **contents ignored by git** | Placeholder |
| [`processed/`](processed/README.md) | Placeholder for feature tables and derived data; **contents ignored by git** | Placeholder |
| [`metadata/`](metadata/README.md) | Metadata schema and [`recording_metadata_template.csv`](metadata/recording_metadata_template.csv) | Template only |
| [`examples/`](examples/README.md) | Small, clearly documented example files for tooling tests (planned) | Placeholder |

## Dataset policy

### 1. Large raw data is not committed

Raw recordings (multi-channel sample arrays, raw audio) are large binary files. They **must not be
committed** to this repository. `.gitignore` excludes `datasets/raw/*` and `datasets/processed/*` except
the READMEs, as well as common audio and binary array formats. Raw data is stored in an external data
directory or storage service and referenced by `recording_id` in the metadata. If a curated dataset is
ever published, it will be released as a separate, versioned archive with its own documentation.

### 2. Stable file naming

Every recording is a **measurement run** with a unique, stable `recording_id`. Preliminary rule:

```text
<YYYYMMDD>_<bearing_id>_<test_condition>_<severity>_<rpm_setpoint>_<seq>
e.g. 20260301_BRG03_imbalance_s2_1500_01   (illustrative format only; not a real recording)
```

Files belonging to a run carry the `recording_id` as prefix followed by the channel name and format,
for example `<recording_id>_accel.npy`, `<recording_id>_acoustic.npy`, `<recording_id>_temp.csv`,
`<recording_id>_rpm.csv`, and `<recording_id>_meta.json`. Identifiers are never reused or renamed after
a run has been recorded. TODO: finalise the rule before the first campaign.

### 3. Splits are by complete measurement run

Training, validation, and test sets **must be split by complete measurement run**. Windows or samples
from the same run **must not** be randomly distributed across different partitions, because adjacent
windows are highly correlated and would leak information, producing optimistic and misleading results.
The partition of each run is recorded in the `dataset_split` metadata column and enforced by the
training tooling. Ideally, different bearing specimens are also kept separate between partitions.

### 4. Metadata is mandatory

Every run must have a metadata record identifying at least: the bearing (`bearing_id`), RPM, load
level, sensor positions, ambient temperature, housing temperature, test condition, severity, and the run
identifier. The complete schema is in [`metadata/README.md`](metadata/README.md). Runs without complete
metadata are not used for training or evaluation.

### 5. Raw audio retention

Raw audio from an airborne microphone may capture speech. Raw audio **should not be permanently
retained** unless required for the project and legally appropriate in the jurisdiction where it is
recorded. The default is to keep only derived features; if raw audio is kept temporarily for analysis,
it is stored in the external data directory, marked in the metadata, and deleted after the retention
period. A piezoelectric contact sensor would reduce this concern.

### 6. Synthetic and augmented data must be labelled

If generated or synthetic data (simulated signals, augmented recordings) is ever used, it must be
clearly labelled as such in the metadata (planned column `data_origin` = `measured` | `augmented` |
`synthetic`) and in any documentation or results that include it. Synthetic data must never be
presented as measured data.

### 7. No fabricated data in the repository

Templates contain headers only. Illustrative examples are clearly marked as such and are never
presented as real recordings.

## Current status

- Policy defined; naming rule preliminary; no recordings.

## TODO

- [ ] Finalise the `recording_id` rule and the controlled vocabularies for conditions, severities, and positions.
- [ ] Choose the external storage location and document access in `raw/README.md`.
- [ ] Add `data_origin` to the metadata template if synthetic data becomes a possibility.
- [ ] Create validation tooling for the metadata CSV in `tools/data_capture/`.
