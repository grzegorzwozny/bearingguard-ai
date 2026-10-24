# Model Training Tools (`tools/model_training`)

**Status: Placeholder** - no training code exists; no model has been trained.

## Purpose

This directory will contain the scripts that train, evaluate, and export the bearing anomaly model from
feature tables produced by `tools/feature_extraction/`. Experiment records live in
[`../../models/training/`](../../models/training/README.md); exported artifacts go to
[`../../models/exported/`](../../models/exported/README.md); evaluation summaries go to
[`../../models/evaluation/`](../../models/evaluation/README.md).

## Expected files

| File | Planned content |
|---|---|
| `split.py` | Build train/validation/test partitions **by run** from the metadata CSV; verify no run appears twice |
| `baseline_stats.py` | Fit the Stage 1 statistical model: per-feature (and per RPM bin) mean and covariance from healthy training runs; produce the normalisation parameters |
| `train_autoencoder.py` | Train the optional Stage 2 neural model on healthy training runs only |
| `evaluate.py` | Compute metrics defined in `models/evaluation/metrics.md`; per-condition, per-severity, per-RPM breakdowns; threshold selection on validation runs |
| `export.py` | Convert the chosen model to TFLite with integer quantisation, generate the C array and parameter JSON, write the export report |
| `configs/` | Reference to experiment configs stored in `models/training/configs/` |
| `requirements.txt` | Pinned dependencies (framework choice TODO) |

## Planned framework options

| Option | Considerations |
|---|---|
| TensorFlow / Keras + TFLite Micro | Mature embedded path, Zephyr module available for TFLM |
| Edge Impulse | Integrated data management, training, and nRF Connect SDK export; less control over the pipeline |
| scikit-learn (Stage 1 only) | Simple statistical detector; parameters exported as plain C constants |

The decision is open and will be made after the first data exists.

## Rules

- No tuning on the test partition.
- Random seeds fixed and recorded.
- Scripts fail loudly if the feature table's `FEATURE_VERSION` does not match the expected version.

## Current status

- No code; framework not selected.

## TODO

- [ ] Choose the framework and export path.
- [ ] Implement `split.py` and `baseline_stats.py` first.
- [ ] Implement `evaluate.py` against the protocol in `models/evaluation/`.
- [ ] Implement `export.py` and validate the quantised model against the float model.
