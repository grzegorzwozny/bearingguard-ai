# Edge AI Module (`firmware/edge_ai`)

**Status: Placeholder** - no inference code exists and no model has been trained.

## Purpose

This directory will contain the on-device anomaly-detection stage: normalisation of the fused feature
vector against RPM and temperature, baseline learning, inference with the deployed model, conversion
of the anomaly score into the Bearing Health Score and condition level, and generation of the
maintenance recommendation. The planning document is
[`../../docs/edge_ai_plan.md`](../../docs/edge_ai_plan.md); the model itself is described in
[`../../models/model_cards/bearing_anomaly_model.md`](../../models/model_cards/bearing_anomaly_model.md).

## Expected files

| File | Planned content |
|---|---|
| `ai_normalize.c/.h` | Per-feature standardisation using baseline statistics; RPM-bin or regression-based normalisation; temperature compensation |
| `ai_baseline.c/.h` | Baseline learning: running mean/variance per feature (and per RPM bin), coverage tracking, persistence via the settings subsystem |
| `ai_model_stat.c/.h` | First-stage statistical model: feature-space distance (for example Mahalanobis distance) from the healthy baseline |
| `ai_model_nn.c/.h` | Optional second-stage neural model (small autoencoder or one-class network) via the chosen runtime |
| `ai_runtime_*.c` | Runtime glue for TensorFlow Lite for Microcontrollers or an Edge Impulse SDK export, including the tensor arena |
| `ai_score.c/.h` | Anomaly score smoothing, Bearing Health Score (0-100) mapping, hysteresis, condition-level thresholds, trend estimation |
| `ai_recommend.c/.h` | Maintenance recommendation text/enum derived from condition level, trend, and dominant contributing features |
| `model/` | Exported model data (generated header); **not committed** unless intentionally published (see `.gitignore`) |
| `Kconfig` | Model selection, arena size, thresholds, smoothing constants |
| `CMakeLists.txt` | Adds the sources and the runtime |

## Planned approach

1. **Baseline first.** The first deliverable is a statistical anomaly detector that requires only the
   learned healthy baseline - no offline training. This provides an immediately useful reference and a
   fallback if the neural model does not fit or does not generalise.
2. **Neural model second.** If the statistical detector proves insufficient on the controlled fault
   conditions, a small autoencoder or one-class model trained offline on healthy data will be deployed.
3. **Explainability.** The module will report which feature group (vibration, acoustic, thermal)
   contributes most to the anomaly, so that recommendations can be more specific.

## Planned runtime constraints

| Constraint | Plan |
|---|---|
| Memory | Model and tensor arena sized to fit comfortably in the nRF54LM20A RAM alongside sample buffers; exact budget TODO |
| Latency | One inference per evaluation period; a few milliseconds is acceptable |
| Determinism | Inference runs in the processing thread, never in interrupt context |
| Updates | Model and thresholds updatable over the debugger or a future DFU; BLE-based model updates are out of scope for the first version |

## Current status

- No code exists; no model exists; no runtime has been selected.

## TODO

- [ ] Select the inference runtime and verify it builds for the target.
- [ ] Define the baseline-learning procedure (duration, speed coverage, acceptance criteria).
- [ ] Implement the statistical detector and the health-score mapping with hysteresis.
- [ ] Define the condition-level thresholds after baseline and fault data exist.
- [ ] Integrate the exported neural model if required by evaluation results.
