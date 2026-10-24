# Model Card: Bearing Anomaly Model

| Field | Value |
|---|---|
| Model name | BearingGuard AI Bearing Anomaly Model |
| Version | none (no version has been trained) |
| **Status** | **Not yet trained - Planned** |
| Model type (planned) | Stage 1: statistical feature-space anomaly detector; Stage 2 (optional): small unsupervised neural network (autoencoder or one-class model) |
| Target platform | Nordic nRF54LM20 DK (Arm Cortex-M33), on-device inference |
| License | Apache-2.0 (same as the repository) |
| Last updated | Repository scaffold (concept stage) |

> **This model card is a placeholder.** It defines the sections that will be completed once a model
> exists. Every statement below describes intent, not achieved behaviour. No training data has been
> collected and no performance has been measured.

## 1. Model purpose

The model is intended to detect **deviations from the learned healthy operating condition** of a metal
rolling-element bearing on the BearingGuard AI test rig, using fused features derived from three-axis
vibration, acoustic signal, bearing-housing temperature, and rotational speed. Its output is an anomaly
score that the firmware converts into a Bearing Health Score and a four-level condition indicator.

## 2. Current status

- **Training status:** not started.
- **Data status:** no recordings exist; the data-collection plan is in
  [`../../docs/data_collection_plan.md`](../../docs/data_collection_plan.md).
- **Deployment status:** not deployed; firmware integration is described in
  [`../../firmware/edge_ai/README.md`](../../firmware/edge_ai/README.md).

| Version | Date | Data used (run IDs) | Evaluation summary | Notes |
|---|---|---|---|---|
| - | - | - | - | No versions exist |

## 3. Intended use

- Research and educational demonstrator of embedded anomaly detection for predictive maintenance.
- Monitoring a **single, known bearing** on the project test rig after a supervised baseline-learning
  phase on that same installation.
- Producing **advisory** condition levels and maintenance recommendations for a human operator.

## 4. Out-of-scope use

- Any safety function: emergency shutdown, interlocking, or protection of people or equipment.
- Monitoring of machines, bearing types, mounting arrangements, or speed/load ranges not covered by the
  learned baseline without a new baseline-learning phase.
- Fault-type classification (for example distinguishing inner-race from outer-race defects) in the
  first iteration.
- Remaining-useful-life prediction.
- Use in certified industrial condition-monitoring or protection systems.

## 5. Expected input features (planned)

Fused feature vector computed by `firmware/dsp/` per evaluation period (preliminary list; final
definition will be frozen in `dsp_feature_vector.h`):

| Group | Features |
|---|---|
| Vibration (per axis and combined) | RMS, peak-to-peak acceleration, crest factor, kurtosis, impulse count, spectral-band energies |
| Acoustic | acoustic RMS, acoustic-band energies |
| Thermal | temperature above ambient, temperature rise rate |
| Operating point | RPM, load level (if available) |

Inputs are standardised against the healthy-baseline statistics, conditioned on RPM (bins or regression)
and compensated for ambient temperature before inference.

## 6. Output anomaly score (planned)

- A non-negative scalar; larger values indicate a larger deviation from the healthy baseline.
- Stage 1: feature-space distance (for example Mahalanobis distance) from the baseline distribution.
- Stage 2: reconstruction error or distance to the learned normal region.
- The score is smoothed over several evaluation periods before mapping to a condition level.
- The model will also report the dominant contributing feature group for explainability.

## 7. Condition-level mapping (planned)

| Condition level | Planned meaning | Threshold |
|---|---|---|
| Green | within the healthy baseline distribution | TODO |
| Yellow | small, sustained deviation | TODO |
| Orange | significant, persistent deviation | TODO |
| Red | severe deviation and/or rapid deterioration trend | TODO |

Thresholds will be derived from the anomaly-score distribution of held-out healthy runs (false-alarm
budget) and adjusted using validation runs with controlled faults. Hysteresis and minimum dwell times
will be applied to avoid flickering. The Bearing Health Score (0-100) will be a monotonic mapping of the
smoothed anomaly score; the mapping function is TODO.

## 8. Training data (planned)

- Source: recordings from the BearingGuard AI test rig only.
- Healthy baseline runs across the planned speed range and load levels, multiple bearing specimens.
- Controlled fault conditions (imbalance, misalignment, loose mounting, increased load, pre-worn
  bearing) at several severity levels - used for validation and testing, not for training the
  unsupervised model.
- Partitioned **by complete measurement run** according to the `dataset_split` metadata column.
- No public datasets are planned for the first iteration; if any are used later, they will be cited here.
- Any synthetic or augmented data will be labelled as such and listed here.

## 9. Validation approach (planned)

- Protocol defined in [`../evaluation/README.md`](../evaluation/README.md).
- Metrics: anomaly-score separation between healthy and each fault condition, false-positive rate on
  held-out healthy runs, detection delay, health-score stability over long healthy runs.
- Per-condition, per-severity, and per-RPM reporting.
- Thresholds selected on validation runs; results reported on untouched test runs.

## 10. False-positive and false-negative considerations

- **False positives** (healthy flagged as degraded) undermine trust and lead to ignored alerts. Primary
  mitigations: RPM/temperature normalisation, baseline coverage of the full operating range, smoothing,
  hysteresis, and a conservative false-alarm budget.
- **False negatives** (degradation missed) are limited by sensor placement, feature choice, and the
  subtlety of early faults. Mitigation: multisensor fusion and trend analysis rather than instantaneous
  thresholds.
- Because the device is advisory only, both error types carry operational rather than safety
  consequences, but the model must never be presented as a protective system.

## 11. RPM dependence

Vibration and acoustic features scale strongly with rotational speed. The model is only valid within the
speed range covered during baseline learning. Operation outside this range will be reported as
"outside learned range" rather than as a bearing anomaly. Order-normalised spectral features are
planned to reduce, not eliminate, this dependence.

## 12. Environmental limitations

- Ambient temperature changes affect the thermal features; compensation uses the ambient sensor and is
  limited to the range seen during baseline learning.
- External vibration (adjacent machinery, handling the bench) and ambient noise contaminate the
  signals; the rig is assumed to be on a stable surface in a quiet laboratory.
- Sensor remounting, cable changes, or guard changes alter the vibration transfer path and may require
  a new baseline.

## 13. Embedded deployment constraints

- Must fit, together with sample buffers and the Bluetooth stack, within the RAM and non-volatile
  memory of the nRF54LM20A; exact budget TODO.
- Inference once per evaluation period in the processing thread; latency of a few milliseconds is acceptable.
- Integer quantisation planned for the neural candidate; quantisation error must be verified against
  the float model.
- Model updates via the debugger or a future DFU mechanism; no over-the-air model update in the first iteration.

## 14. Ethical and safety considerations

- The model does not process personal data; the acoustic channel is reduced to energy features on the
  device, and raw audio is not retained outside controlled development captures.
- Outputs are advisory. Misuse as a protective function is explicitly out of scope and documented in
  the repository disclaimer and [`../../docs/safety.md`](../../docs/safety.md).
- Results will be reported honestly, including failure cases and limitations.

## 15. Known limitations

- Trained (when trained) on one rig, one bearing type, and artificially induced conditions; no claim of
  transfer to other machines.
- Cannot distinguish fault types in the first iteration.
- Cannot predict remaining useful life.
- Baseline learning requires a period of known-healthy operation, which must be assured by the operator.
- Sensitivity to mounting and installation variation.

## 16. Future updates

- Complete sections 2, 8, and 9 with real data and results after the first training experiment.
- Add fault-type indication if supervised data proves sufficient.
- Investigate transfer of baselines between bearing specimens of the same type.
- Investigate longer-term trend features for degradation-rate estimation.

## TODO

- [ ] Freeze the feature vector definition.
- [ ] Collect healthy-baseline and controlled-fault data.
- [ ] Train Stage 1 and evaluate; decide on Stage 2.
- [ ] Fill in thresholds, metrics, and version table; remove the "not yet trained" status only when true.
