# Datasheets (`hardware/datasheets`)

**Status: Placeholder** - no components selected, so no datasheet references exist yet.

## Purpose

This directory provides an **index of links** to the official documentation of every component used
in BearingGuard AI. It exists so that reviewers and contributors can find the authoritative source for
each part quickly.

## Policy: links, not copies

Datasheets, user guides, and application notes are copyrighted by their manufacturers. **Do not commit
copies of datasheets or other proprietary documents to this repository.** Record the official URL, the
document title, the revision or date, and the specific sections that were relied on.

## Expected files

| File | Planned content |
|---|---|
| `datasheet_index.md` | Table with `Component, Manufacturer, Document title, Revision/date, Official URL, Sections used, Notes` |
| `design_parameters.md` | The specific numbers taken from datasheets and used in the design (e.g. accelerometer bandwidth, noise density, sensor supply voltage, DK I/O voltage), each with a reference to the index |

## Planned entries

| Component | Expected documents |
|---|---|
| Nordic nRF54LM20 DK | DK hardware user guide, nRF54LM20A product specification, nRF Connect SDK board documentation |
| Accelerometer | Datasheet, application note on mounting and FIFO use |
| Acoustic sensor | MEMS microphone datasheet (PDM timing, acoustic overload point) or piezo element datasheet |
| Temperature sensors | Datasheet (accuracy, response time) or NTC curve data |
| RPM sensor | Datasheet (output type, air gap or sensing distance, supply voltage) |
| Motor and driver | Datasheets (voltage, speed-torque, current limits) |
| Bearings | Manufacturer catalogue data (geometry needed to compute characteristic defect frequencies) |

## Current status

- Empty index; no parts selected.

## TODO

- [ ] Create `datasheet_index.md` as soon as the first component is shortlisted.
- [ ] Record bearing geometry (ball count, ball diameter, pitch diameter, contact angle) from the manufacturer catalogue for later defect-frequency analysis.
- [ ] Record the DK I/O voltage and header pinout references used by `hardware/wiring/` and `firmware/boards/`.
