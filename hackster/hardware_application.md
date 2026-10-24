# Hardware Application - Draft Answers

**Status: Draft.** Clearly separated draft answers for a hardware-application form. Review every answer
for unsupported claims before submission. The personal-background answer is a placeholder and must be
replaced by the applicant.

---

## Title of your idea

BearingGuard AI: Early Bearing Fault Detection - a Bluetooth Edge AI node for predictive maintenance
of rotating machinery.

---

## What are you going to build?

A compact, wireless condition-monitoring demonstrator based on the Nordic nRF54LM20 DK that is mounted
at a metal ball bearing and combines three-axis vibration, acoustic, bearing-housing temperature, and
rotational-speed sensing. The device will learn the healthy operating signature of the bearing during a
supervised baseline phase, run an Edge AI anomaly-detection model locally, and report a Bearing Health
Score, a green/yellow/orange/red condition level, feature trends, and maintenance recommendations over
Bluetooth Low Energy to a dashboard. To develop and demonstrate it safely, I will build a small guarded
bench-top test rig with replaceable bearings on which healthy and controlled deviation conditions
(imbalance, misalignment, loose mounting, increased load, pre-worn bearing) can be reproduced.

---

## What problem will it solve?

Bearing degradation is one of the most common causes of unplanned machine downtime, yet most small and
medium machines are not monitored at all. Early signs - subtle changes in vibration, sound, and
temperature - appear long before failure but are missed by periodic inspection, and simple threshold
alarms produce false alarms whenever speed or load changes. BearingGuard AI aims to make early-warning
monitoring accessible: a self-learning node that needs no wiring infrastructure and no vibration expert
to interpret it.

---

## How is it different?

- **Multisensor fusion** of vibration, acoustic, thermal, and speed information instead of vibration alone.
- **Baseline learning on the installed machine** rather than fixed, generic thresholds.
- **RPM and temperature normalisation** to suppress false alarms from normal operating changes.
- **Edge AI on the node**: raw signals stay on the device; only compact features, scores, and alerts are sent.
- **Interpretable output**: a health score, four condition levels, and a stated dominant contributing
  feature group, with an honest "outside learned range" state.
- **Reproducible development**: a documented test rig, run-level dataset splits, and a model card.

---

## Why is it useful?

It gives maintenance staff lead time. Detecting deviation early allows bearings to be replaced during a
planned stop instead of after a failure, avoids collateral damage to shafts, housings, and motors,
reduces scrap and emergency logistics, and avoids discarding healthy bearings on a fixed schedule. For
developers and students it provides an open, documented reference for embedded anomaly detection on a
modern low-power Bluetooth SoC.

---

## How does it address predictive maintenance?

Predictive maintenance means intervening when the condition of the asset indicates developing
degradation. BearingGuard AI monitors condition continuously, scores deviation from the learned healthy
state, tracks the trend, and escalates through yellow, orange, and red levels with corresponding
recommendations (observe, plan inspection, stop for inspection). The first objective is reliable anomaly
detection relative to the baseline; fault-type classification and remaining-useful-life estimation are
explicitly deferred to future work.

---

## How will Bluetooth be used?

Bluetooth Low Energy is the reporting and configuration channel. A custom Bearing Health GATT service
will expose Bearing Health Score, Condition Level, Vibration RMS, Vibration Crest Factor, Acoustic
Energy, Housing Temperature, RPM, Anomaly Score, Maintenance Recommendation, Device Status, Baseline
Learning Control, and Diagnostic Capture Control. Clients receive periodic notifications and immediate
alerts on level changes; authenticated writes start baseline learning or a bounded diagnostic capture.
Bluetooth never controls the machine.

---

## How will Edge AI be used?

On the device, sensor data passes through validation, filtering, windowing, time- and frequency-domain
feature extraction, RPM and temperature normalisation, and multisensor fusion into an anomaly model.
The plan is staged: a transparent statistical detector that uses only the learned baseline comes first;
a small autoencoder or one-class model trained offline on healthy data and deployed with integer
quantisation follows if needed. The anomaly score is smoothed and mapped to the health score and
condition level with hysteresis. No model has been trained yet.

---

## How will the nRF54LM20 DK be used?

The nRF54LM20 DK will be the central platform: its SPI/I2C, PDM, SAADC, and timer peripherals acquire the
sensors and RPM pulses; the Arm Cortex-M33 performs DSP, feature extraction, and Edge AI inference; its
Bluetooth LE radio provides the Bearing Health Service; on-chip non-volatile memory stores the learned
baseline and settings; and the on-board debugger, logging, and current-measurement features support
development and power profiling. Firmware will be built with the nRF Connect SDK (Zephyr). The DK has
not yet been acquired; specifications will be verified against official documentation.

---

## Tell us about yourself

[TODO: Replace with the applicant's final personal background before submission.]

---

## Pre-submission checklist

- [ ] Personal background placeholder replaced.
- [ ] All answers reviewed for unsupported claims (no completed hardware, data, firmware, or model).
- [ ] Project status stated as concept and planning stage.
- [ ] Safety and advisory-only statements present.
