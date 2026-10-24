# Documentation

**Status: Planning documents** - everything in this directory describes proposed and planned work.
The project is at the concept stage; no document reports completed hardware, measurements, firmware,
or model results.

## Documents

| Document | Content | Status |
|---|---|---|
| [`architecture.md`](architecture.md) | Preliminary system architecture: layers, components, interfaces, data flow, state machine, LED indication | Draft |
| [`project_plan.md`](project_plan.md) | Milestones, work packages, dependencies, risks, and decision points | Draft |
| [`test_rig_plan.md`](test_rig_plan.md) | Bench-top test rig: motor, coupling, shaft, bearing supports, load, imbalance disk, RPM sensor, sensor positions, base plate, emergency stop, guard, speed limit | Draft |
| [`data_collection_plan.md`](data_collection_plan.md) | Recording campaigns, test matrix, run structure, metadata, splits, retention | Draft |
| [`bluetooth_service_plan.md`](bluetooth_service_plan.md) | Preliminary BLE architecture and Bearing Health Service characteristics (UUIDs TODO) | Draft |
| [`edge_ai_plan.md`](edge_ai_plan.md) | Processing flow from sensor acquisition to BLE notification; features; model strategy | Draft |
| [`safety.md`](safety.md) | Safety requirements for the rig and the limits of the device's role | Draft |
| [`sustainability.md`](sustainability.md) | Expected sustainability impact and how it could be assessed | Draft |
| [`limitations.md`](limitations.md) | Known and expected limitations of the approach and the demonstrator | Draft |

## Conventions

- Status markers: `Status: Planned`, `Status: Placeholder`, `Status: Draft`, and `TODO` items.
- Numeric parameters that have not been determined are written as `TODO`, never guessed.
- Diagrams are written in Mermaid so they render on GitHub and can be reviewed as text.
- Documents link to the directory READMEs that will hold the corresponding implementation.

## Planned additions

| Document | Purpose |
|---|---|
| `firmware_design.md` | Detailed firmware design once the skeleton exists (threads, buffers, timing budget) |
| `signal_analysis_findings.md` | Results of the first signal-analysis campaign that fix sample rates and feature bands |
| `calibration_procedures.md` | Sensor offset calibration, accelerometer orientation check, RPM sensor alignment |
| `user_guide.md` | How to install, baseline, and monitor with the finished demonstrator |

## TODO

- [ ] Review all drafts for consistency after the first design decisions (sensor selection, SDK version).
- [ ] Add the planned documents as the corresponding work packages start.
