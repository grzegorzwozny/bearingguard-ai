# Processed Data (`datasets/processed`)

**Status: Placeholder** - no processed data exists. Everything in this directory except this README is
ignored by git.

## Purpose

This directory marks where derived data - per-window feature tables, normalised feature sets, and
partition lists - would live in a local working copy. Processed data is regenerated from raw data by
the versioned tooling, so it is not committed; what *is* committed is the description of how to
regenerate it.

## Expected local layout (not committed)

```text
datasets/processed/
├── README.md                                   (this file - the only tracked file)
├── features_v<FEATURE_VERSION>/
│   ├── <recording_id>_features.parquet         one row per window: features + run metadata columns
│   └── manifest.json                           feature version, tool version, list of runs, creation time
└── splits/
    └── split_<name>.json                       lists of recording_ids for train / validation / test
```

## Rules

- Every feature table records the `FEATURE_VERSION` of the extraction code and the firmware feature
  specification it matches.
- Partition files list **complete runs** only; they are the input to all training and evaluation.
- Processed data is disposable: if it cannot be regenerated from raw data and committed code, the
  pipeline is broken and must be fixed.

## Current status

- Empty by design.

## TODO

- [ ] Fix the feature table schema with `tools/feature_extraction/`.
- [ ] Define the split file format with `tools/model_training/split.py`.
