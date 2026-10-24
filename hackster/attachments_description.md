# Hackster Attachments Description

**Status: Draft.** This document lists which **future** files will be linked or uploaded to the
Hackster.io attachments sections. None of these files exist yet; the list defines what will be published
and under which section once the corresponding milestone is reached.

## General rules

- Prefer **links to the GitHub repository** over uploads, so that Hackster always points to the current
  version and the full history.
- Upload only the project's own work. Never upload datasheets, manufacturer schematics, or other
  third-party copyrighted material.
- Upload only small, reviewed artifacts; large data, raw audio, trained model binaries, and videos are
  not uploaded (videos are linked from a hosting platform).
- Every attachment carries a short description with its status (planned, draft, reviewed, final).

## Code

| Attachment | Source in repository | Milestone | Notes |
|---|---|---|---|
| Repository link | Root of the GitHub repository | M0 | Primary code attachment; link only |
| Firmware application | `firmware/app/`, `firmware/boards/`, `firmware/drivers/`, `firmware/dsp/`, `firmware/edge_ai/`, `firmware/bluetooth/` | M8-M9 | Link to the firmware directory and the release tag |
| West manifest | `firmware/west.yml.example` -> `west.yml` | M3 | Link |
| Data capture tool | `tools/data_capture/` | M4 | Link |
| Feature extraction (Python reference) | `tools/feature_extraction/` | M5 | Link |
| Model training and export scripts | `tools/model_training/` | M7 | Link |
| BLE dashboard | `tools/ble_dashboard/` | M9 | Link |
| Model card | `models/model_cards/bearing_anomaly_model.md` | M7 | Link; the trained model binary itself is published via a GitHub Release if at all |

## Schematics and circuit diagrams

| Attachment | Source in repository | Milestone | Notes |
|---|---|---|---|
| Electrical block diagram | `media/diagrams/electrical_block_diagram.png` (from `hardware/block_diagrams/`) | M1-M2 | Upload PNG/SVG |
| Sensor interface schematic | `hardware/schematics/sensor_interface.kicad_sch` + exported PDF | M3 | Upload the PDF export of the reviewed revision; link KiCad source |
| Piezo front end (if used) | `hardware/schematics/piezo_front_end.kicad_sch` + PDF | M5 | Conditional |
| NTC divider (if used) | `hardware/schematics/ntc_divider.kicad_sch` + PDF | M3 | Conditional |
| RPM sensor interface | `hardware/schematics/rpm_sensor_interface.kicad_sch` + PDF | M3 | |
| Wiring table | `hardware/wiring/wiring_table.csv` | M3 | Link |
| Sensor carrier PCB (if made) | `hardware/pcb/` | After M3 | Conditional; link to KiCad project and fabrication outputs |

## CAD, enclosures, and custom parts

| Attachment | Source in repository | Milestone | Notes |
|---|---|---|---|
| Rig assembly | `mechanical/cad/rig_assembly.step` | M2 | Upload STEP if small enough, otherwise link |
| Sensor brackets | `mechanical/cad/parts/*.stl`, `*.step` | M2 | Upload STL for printable parts |
| Imbalance disk | `mechanical/cad/parts/imbalance_disk.step` + `mechanical/drawings/imbalance_disk.pdf` | M2 | Include the maximum-mass marking in the drawing |
| Instrumented support adapter | `mechanical/cad/parts/` + drawing | M2 | |
| Transparent guard | `mechanical/cad/parts/guard_*.step` + `mechanical/drawings/guard_panels.pdf` | M2 | Attach the guard requirements document as well |
| Drawings index | `mechanical/drawings/README.md` | M2 | Link |

## Other media (story body, not attachments)

| Item | Source | Milestone |
|---|---|---|
| Cover image | `media/cover/bearingguard_cover.png` | M0-M1 (concept), M2+ (photo) |
| System and pipeline diagrams | `media/diagrams/*.png` | M0-M1 |
| Rig and sensor photos | `media/photos/` | M2+ |
| Demonstration video | Hosted link from `media/video/video_index.md` | M10 |

## Current status

- No attachments exist; only the repository link can be provided at this stage.

## TODO

- [ ] Export the concept diagrams for the initial Hackster entry.
- [ ] Update this list as decisions (piezo vs. microphone, carrier PCB) are made.
- [ ] Review every attachment for third-party content before upload.
