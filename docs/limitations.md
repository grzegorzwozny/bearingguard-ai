# Limitations

**Status: Draft.** This document lists the known and expected limitations of BearingGuard AI so that
readers do not over-interpret the concept, the planned demonstrator, or future results. It will be
extended with observed limitations as the project progresses.

## 1. Project-status limitations

- The project is at the **concept and planning stage**: no hardware has been assembled, no data has
  been recorded, no firmware is functional, and no model has been trained.
- All architecture, parameters, and behaviours in this repository are proposals and may change.
- No performance figure exists; none will be quoted until produced by the documented evaluation protocol.

## 2. Scope limitations

- **Anomaly detection only.** The first objective is to detect deviation from a learned healthy
  baseline, not to classify fault types (inner race, outer race, rolling element, cage, lubrication)
  or to localise the fault.
- **No remaining-useful-life prediction.** RUL estimation needs run-to-failure data from many
  specimens; this is out of scope.
- **Single bearing, single rig.** The demonstrator monitors one instrumented bearing on one rig.
- **Advisory output.** Health score and recommendation are information for a human; no control or
  protection function is provided or implied.

## 3. Methodological limitations

- **Artificially induced conditions.** Imbalance, misalignment, loose mounting, increased load, and
  pre-worn bearings are produced deliberately and quickly; real degradation develops slowly and
  combines several mechanisms. Results on the rig may not transfer to field failures.
- **Baseline dependence.** The system is only as good as its baseline: if the bearing was already
  degraded, misaligned, or poorly mounted during baseline learning, that state is learned as "healthy".
- **Operating-range dependence.** The model is valid only within the speed, load, and temperature range
  covered during baseline learning; outside it, the device reports "outside learned range".
- **Small dataset.** A laboratory campaign yields a limited number of runs and specimens; statistical
  confidence will be limited and must be reported honestly.
- **Run-level evaluation.** Even with correct run-level splits, runs recorded on the same rig and days
  share environmental factors; generalisation claims must be cautious.

## 4. Physical and sensing limitations

- **Mounting dominates.** Accelerometer mounting method, surface quality, and position strongly affect
  usable bandwidth and repeatability; remounting may require a new baseline.
- **Rig resonances.** The base plate, supports, and guard have their own resonances that can mask or
  mimic bearing-related content.
- **Acoustic contamination.** Motor noise, coupling noise, and laboratory background affect the acoustic
  channel; an airborne microphone is especially sensitive to the environment.
- **Thermal lag.** Temperature responds slowly and depends on load, ambient conditions, and airflow.
- **RPM measurement.** One pulse per revolution gives coarse speed updates at low speed.
- **Sensor quality.** Low-cost MEMS sensors have higher noise and lower bandwidth than industrial
  accelerometers and acoustic-emission sensors.

## 5. Embedded limitations

- RAM, non-volatile memory, and processing time on the nRF54LM20A bound sample rates, window lengths,
  feature count, and model size.
- Integer quantisation of a neural model introduces error that must be verified.
- Baseline statistics stored on the device are per installation and are lost if settings are erased
  without backup.

## 6. Bluetooth limitations

- Range and reliability depend on the environment; BLE is not a real-time control channel and is not
  used as one.
- The service is custom and preliminary; interoperability with existing condition-monitoring systems
  is not provided.
- Security depends on correct pairing; an unpaired client cannot change settings but a demo-friendly
  profile may allow unencrypted reads (decision pending).

## 7. Safety and regulatory limitations

- BearingGuard AI is not certified for any safety, protection, or industrial function and must not be
  used as such.
- The test rig is a laboratory device and must only be operated according to
  [`safety.md`](safety.md) after a risk assessment.
- Operation in any location must comply with local regulations, including those on audio recording.

## 8. Documentation limitations

- Component specifications quoted for the nRF54LM20 DK and other parts are taken from public product
  information and must be verified against official documentation before design decisions.
- Any numeric placeholder marked `TODO` is unknown, not estimated.

## TODO

- [ ] Add observed limitations from each milestone (rig characterisation, bring-up, campaigns, evaluation).
- [ ] Revisit the scope section if fault-type indication becomes feasible.
