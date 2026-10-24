# Models

**Status: Planned** - no model has been trained. No model files exist.

## Purpose

This directory documents the machine-learning side of BearingGuard AI: how the anomaly-detection model
will be trained, exported, evaluated, and described. The Edge AI concept is defined in
[`../docs/edge_ai_plan.md`](../docs/edge_ai_plan.md); the on-device integration is described in
[`../firmware/edge_ai/README.md`](../firmware/edge_ai/README.md).

## Directory overview

| Directory | Content | Status |
|---|---|---|
| [`training/`](training/README.md) | Training configuration, experiment notes, and references to the training scripts in `tools/model_training/` | Placeholder |
| [`exported/`](exported/README.md) | Exported embedded model artifacts (TFLite / C arrays); **ignored by git** unless intentionally published | Placeholder |
| [`evaluation/`](evaluation/README.md) | Evaluation protocol, metrics definitions, and result summaries (plots/tables, not raw data) | Placeholder |
| [`model_cards/`](model_cards/bearing_anomaly_model.md) | Model cards describing purpose, data, limitations, and status of each model version | Placeholder (not trained) |

## Planned modelling strategy

1. **Statistical baseline detector** - per-feature standardisation against healthy-baseline statistics
   and a feature-space distance score. No offline training beyond baseline statistics; serves as the
   reference and fallback.
2. **Small unsupervised neural model** - autoencoder or one-class network trained only on
   healthy-condition feature vectors; anomaly score = reconstruction error or distance to the learned
   normal region.
3. **Optional supervised refinement** - only if controlled fault data is sufficient and the goal expands
   to distinguishing fault types. Not planned for the first iteration.

The first objective is **anomaly detection relative to a healthy baseline**, not fault classification or
remaining-useful-life prediction.

## Rules

- Trained model binaries are not committed to the main tree; publish intentionally selected artifacts
  via releases or add explicit negation rules in `.gitignore`.
- Every trained model version must have a model card with its data lineage and evaluation summary.
- Evaluation must use run-level dataset splits (see [`../datasets/README.md`](../datasets/README.md)).
- No performance numbers may appear in documentation until produced by a reproducible evaluation.

## Current status

- No data, no training runs, no models.

## TODO

- [ ] Select the training framework and export path (see `tools/model_training/`).
- [ ] Define the feature vector jointly with `firmware/dsp/`.
- [ ] Define evaluation metrics and acceptance criteria in `evaluation/`.
- [ ] Train the first model after the healthy-baseline and fault campaigns.
