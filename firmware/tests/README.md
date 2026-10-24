# Firmware Tests (`firmware/tests`)

**Status: Placeholder** - no tests exist yet because no firmware exists yet.

## Purpose

This directory will contain automated tests for the firmware modules and notes on hardware-in-the-loop
verification. The goal is that signal processing, feature extraction, scoring, and protocol encoding can
be verified on a host machine without the nRF54LM20 DK, so that correctness does not depend on hardware
availability and regressions are caught early.

## Expected layout

```text
firmware/tests/
├── README.md                  This file
├── testcase.yaml              Twister test metadata (planned)
├── dsp/                       Ztest suites for filters, windowing, time/frequency features
├── edge_ai/                   Ztest suites for normalisation, baseline statistics, health-score mapping, hysteresis
├── bluetooth/                 Ztest suites for characteristic encoding/decoding and control-command validation
├── drivers/                   Ztest suites for RPM period-to-speed and stall logic, thermistor conversion
├── fixtures/                  Small synthetic input vectors (sine, impulse, noise) and expected outputs
└── hil/                       Hardware-in-the-loop checklists and scripts (planned, after bring-up)
```

## Planned test strategy

| Level | Tooling | Scope |
|---|---|---|
| Unit (host) | Zephyr Ztest on `native_sim`, run through Twister | Pure functions in `dsp/`, `edge_ai/`, `bluetooth/` encoding, driver maths |
| Equivalence | Ztest + Python | Feature vectors from the C implementation must match the Python reference in `tools/feature_extraction/` within a defined tolerance |
| Integration (target) | Twister on the DK, manual checklist | Sensor self-tests, sampling-rate verification, BLE service discovery with a reference client |
| Hardware-in-the-loop | Test rig, dashboard, checklists in `hil/` | End-to-end behaviour under controlled conditions; results recorded with the **Hardware test** issue template |

## Rules

- Tests use **synthetic** signals or small, clearly documented fixture files; no fabricated
  "measurement" data may be presented as real.
- Any numeric result quoted in documentation must come from a reproducible test or recorded run.
- Hardware-in-the-loop sessions must follow the safety checklist in
  [`../../docs/safety.md`](../../docs/safety.md).

## Current status

- No tests exist. Twister configuration is planned.

## TODO

- [ ] Create `testcase.yaml` and the first Ztest suite when the DSP module is implemented.
- [ ] Add synthetic fixtures with documented generation scripts.
- [ ] Add a Python/C feature equivalence test.
- [ ] Write the hardware-in-the-loop checklist after the rig and firmware bring-up.
- [ ] Run tests in continuous integration.
