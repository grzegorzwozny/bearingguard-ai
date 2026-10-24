# Raw Data (`datasets/raw`)

**Status: Placeholder** - no recordings exist. Everything in this directory except this README is
ignored by git.

## Purpose

This directory marks where raw recordings would live in a **local working copy**. It documents the
expected layout so that the capture tooling and the analysis tooling agree, but the raw files themselves
are never committed (see the policy in [`../README.md`](../README.md)).

## Expected local layout (not committed)

```text
datasets/raw/
├── README.md                              (this file - the only tracked file)
└── <recording_id>/
    ├── <recording_id>_accel.npy           three-axis acceleration samples, scaled to m/s^2 or g (documented)
    ├── <recording_id>_acoustic.npy        acoustic samples (microphone or piezo), scaled units documented
    ├── <recording_id>_temp.csv            timestamp, housing_temperature_c, ambient_temperature_c
    ├── <recording_id>_rpm.csv             timestamp, rpm (or raw pulse timestamps)
    ├── <recording_id>_meta.json           full run metadata (superset of the metadata CSV row)
    └── <recording_id>_integrity.json      stream integrity report from the capture tool (gaps, saturation flags)
```

## Information every raw run must carry

- Sample rates and scaling per channel.
- Device firmware version and capture configuration.
- Sensor positions and orientation (controlled vocabulary).
- Start and end timestamps, operator, and notes.
- Integrity status (valid / invalid with reason).

## External storage

Raw data will be stored in an external data directory or storage service. TODO: document the storage
location, access procedure, and backup policy here without including credentials.

## Current status

- Empty by design; no recordings.

## TODO

- [ ] Finalise channel file formats and units with `tools/data_capture/`.
- [ ] Document the external storage location and retention policy (especially for raw audio).
