# Model Training (`models/training`)

**Status: Placeholder** - no training has taken place.

## Purpose

This directory will hold the configuration and record of model-training experiments: which data
(by run identifier) was used, which features and preprocessing were applied, hyperparameters, and the
outcome. The executable training code lives in
[`../../tools/model_training/`](../../tools/model_training/README.md); this directory keeps the
*reproducibility record*, not the scripts.

## Expected files

| File | Planned content |
|---|---|
| `configs/*.yaml` | One configuration per experiment: dataset split definition (list of run IDs per partition), feature set version, normalisation method, model architecture, hyperparameters, random seeds |
| `experiments.md` | Chronological log: experiment ID, config file, date, short result summary, decision taken |
| `runs/` | Training logs and checkpoints - **ignored by git** |
| `checkpoints/` | Intermediate model checkpoints - **ignored by git** |

## Planned training workflow

1. Select runs for training, validation, and test **by complete measurement run**, using the
   `dataset_split` column of the recording metadata.
2. Extract features with the versioned feature-extraction tool so that on-device and offline features match.
3. Fit the statistical baseline (mean, covariance per RPM bin) on healthy training runs.
4. Train the neural candidate (if used) only on healthy training runs; tune thresholds on validation
   runs that include controlled fault conditions.
5. Evaluate on the held-out test runs; record results in `../evaluation/`.
6. Export the chosen model to the embedded format in `../exported/`.
7. Write or update the model card.

## Rules

- Never tune anything on the test partition.
- Record the exact run IDs used; the metadata CSV is the source of truth.
- Keep configurations small and textual; large logs and checkpoints stay out of the repository.

## Current status

- No configurations, no experiments.

## TODO

- [ ] Define the configuration schema once the feature vector is frozen.
- [ ] Start `experiments.md` with the first baseline experiment after data collection.
