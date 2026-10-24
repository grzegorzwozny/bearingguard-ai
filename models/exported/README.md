# Exported Models (`models/exported`)

**Status: Placeholder** - no model has been exported because none has been trained.

## Purpose

This directory is the destination for models converted into the format consumed by the firmware,
together with the metadata needed to deploy them correctly (feature ordering, normalisation
parameters, thresholds, quantisation details).

## Expected files (per model version)

| File | Planned content |
|---|---|
| `bearing_anomaly_vX.Y.tflite` | Quantised TensorFlow Lite model (if the TFLM route is used) |
| `bearing_anomaly_vX.Y_model_data.h` / `.cc` | C array generated from the model for inclusion in `firmware/edge_ai/model/` |
| `bearing_anomaly_vX.Y_params.json` | Feature order, per-feature mean/scale, RPM-bin definitions, anomaly-score to health-score mapping, condition thresholds, model hash |
| `bearing_anomaly_vX.Y_export_report.md` | Export settings, input/output tensor shapes and types, arena size estimate, and a checksum of the source checkpoint |

## Version-control policy

Everything in this directory except this README is **ignored by git** (`models/exported/*` in
`.gitignore`). Exported models are build artifacts of the training pipeline; they are large, binary,
and must stay linked to a specific training run. When a model version is intentionally published:

- attach it to a GitHub Release, or
- add an explicit negation rule for that one file in `.gitignore` and reference its model card.

## Planned export process

1. Convert the trained model with post-training integer quantisation (if applicable).
2. Verify that quantised outputs match the float model on the validation set within tolerance.
3. Generate the C array and the parameter file.
4. Record the export report and update the model card's "current status" and version table.

## Current status

- Empty by design.

## TODO

- [ ] Define the parameter-file schema jointly with `firmware/edge_ai/`.
- [ ] Add the export script to `tools/model_training/` and document it here.
