# Recording Metadata (`datasets/metadata`)

**Status: Template only** - the schema is defined; no metadata rows exist because no recordings exist.

## Purpose

This directory defines the metadata that must accompany every measurement run. Metadata makes
recordings interpretable (what bearing, what condition, what speed), enables correct run-level dataset
splits, and allows results to be broken down per condition, severity, and operating point.

## Files

| File | Content |
|---|---|
| [`recording_metadata_template.csv`](recording_metadata_template.csv) | Header-only CSV template; one row per measurement run will be appended by the capture tooling |
| `recording_metadata.csv` (planned, external or committed) | The populated metadata table. Small enough to commit if it contains no personal data; decision TODO |
| `vocabularies.md` (planned) | Controlled vocabularies for `test_condition`, `severity`, `accelerometer_position`, `acoustic_sensor_type`, `acoustic_sensor_position`, `dataset_split` |

## Column definitions

| Column | Type | Description |
|---|---|---|
| `recording_id` | string | Unique, stable run identifier (see naming rule in [`../README.md`](../README.md)) |
| `bearing_id` | string | Identifier of the physical bearing specimen (label on the bearing / rig log) |
| `timestamp` | ISO 8601 | Start time of the run, with timezone offset |
| `test_condition` | enum | `healthy_baseline`, `imbalance`, `misalignment`, `loose_mounting`, `increased_load`, `pre_worn_bearing` (preliminary vocabulary) |
| `severity` | enum | `none`, `s1`, `s2`, `s3` (preliminary; defined per condition in the test-rig plan, e.g. imbalance mass step, shim thickness, torque reduction) |
| `rpm` | number | Measured mean shaft speed during the run (set-point recorded in notes if different) |
| `load_level` | enum or number | Indexed setting of the adjustable load / brake (`L0`-`L3` preliminary) or measured value if available |
| `accelerometer_position` | enum | Controlled vocabulary, e.g. `support_B_radial_vertical` |
| `acoustic_sensor_type` | enum | `mems_microphone_pdm` or `piezo_contact` |
| `acoustic_sensor_position` | enum | Controlled vocabulary, e.g. `support_B_housing_top`, `airborne_10cm_support_B` |
| `ambient_temperature_c` | number | Ambient temperature at run start, degrees Celsius |
| `housing_temperature_c` | number | Housing temperature at run start, degrees Celsius |
| `sample_rate_hz` | number | Vibration sample rate; acoustic rate recorded in the run's JSON metadata if different |
| `window_duration_ms` | number | Analysis window duration used for feature extraction, or the run duration for raw captures (clarify in notes) |
| `operator_notes` | string | Free text: set-point, anomalies during the run, environmental events, deviations from procedure |
| `dataset_split` | enum | `train`, `validation`, `test`, or `unassigned`; assigned per **complete run** |

Planned additional columns (not yet in the template): `data_origin` (`measured` / `augmented` /
`synthetic`), `firmware_version`, `capture_tool_version`, `run_duration_s`, `integrity_status`,
`raw_audio_retained` (`yes` / `no` / `deleted_<date>`).

## Rules

- Append rows only through the capture tooling or after validation; never edit historical rows except to
  correct documented errors (record corrections in the notes).
- Use the controlled vocabularies; new values must be added to `vocabularies.md` first.
- Do not store personal data in metadata beyond an operator initial or role.
- **Do not add fabricated rows.** The template stays header-only until real runs exist.

## Illustrative example row (documentation only - NOT a recording)

The following line shows the intended format. It is **not** real data and must not be copied into the
metadata file:

```text
20260301_BRG03_imbalance_s2_1500_01,BRG03,2026-03-01T10:15:00+01:00,imbalance,s2,1500,L1,support_B_radial_vertical,mems_microphone_pdm,airborne_10cm_support_B,22.4,27.9,6400,1000,"illustrative example only",unassigned
```

## Current status

- Header-only template created.

## TODO

- [ ] Write `vocabularies.md` with the final controlled vocabularies.
- [ ] Decide whether the populated metadata table is committed or kept with the external data.
- [ ] Add the planned additional columns before the first campaign.
