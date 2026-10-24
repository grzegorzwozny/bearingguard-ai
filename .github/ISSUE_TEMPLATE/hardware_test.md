---
name: Hardware test
about: Record a hardware or test-rig observation, test session, or safety-relevant event
title: "[HW test] "
labels: hardware, test
assignees: ''
---

<!--
Use this template to document test sessions on the rig, sensor bring-up observations, and safety
observations once hardware exists. Record facts, not conclusions about detection capability.
Attach plots or summaries, never raw recordings or raw audio. No personal data.
-->

## Test objective

What was being tested or observed, and which milestone / work package it belongs to.

## Safety checks performed (mandatory for any run with rotating parts)

- [ ] Transparent protective guard fitted and secured
- [ ] Emergency stop tested before the session
- [ ] Controlled maximum speed confirmed in the motor driver
- [ ] Imbalance masses captive and within the permitted maximum
- [ ] Fasteners at the specified torque (or at the documented reduced torque for loose-mounting tests)
- [ ] Loose items removed; cables secured
- [ ] Eye and hearing protection worn
- [ ] Two-person rule observed for fault tests
- [ ] Pre-run checklist recorded

If any box is unchecked, the rig must not have been run. Explain.

## Rig configuration

- Bearing ID(s):
- Test condition and severity:
- Speed set-point(s) [rpm]:
- Load level:
- Sensor positions (controlled vocabulary):
- Firmware version / build configuration:
- Capture tool version:

## Observations

Describe what was observed (sensor readings plausible? integrity report clean? unexpected noise,
heating, vibration, instability?). Attach small plots or summary tables.

## Recordings produced

| recording_id | valid (yes/no) | notes |
|---|---|---|
| | | |

## Issues found

Defects, deviations from procedure, or safety concerns (mark safety concerns clearly with the `safety` label).

## Follow-up actions

- [ ]
- [ ]

## Attachments

Plots, photos (guard fitted!), checklists. No raw data.
