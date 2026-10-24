# Bill of Materials (`hardware/bom`)

**Status: Preliminary** - categories are defined; no exact parts have been selected or purchased.

## Purpose

This directory holds the bill of materials for the BearingGuard AI demonstrator: the processing
platform, sensors, test-rig drive train, fault-injection parts, indication and safety items, and
infrastructure. The BOM is the single list used for purchasing planning and for the Hackster project
page.

## Files

| File | Content |
|---|---|
| [`preliminary_bom.csv`](preliminary_bom.csv) | Preliminary BOM with columns `Category,Item,Quantity,Status,Purpose,Selection Notes` |
| `final_bom.csv` (planned) | Final BOM with manufacturer, part number, supplier, unit price, and link, created after component selection |

## Status values used in the BOM

| Status | Meaning |
|---|---|
| `Planned` | Category and purpose defined; specific part not yet selected or confirmed |
| `Candidate` | One or more specific parts shortlisted; not yet ordered |
| `Confirmed` | Part selected and ordered or available |
| `Received` | Part physically available to the project |

All rows are currently `Planned`, including the Nordic nRF54LM20 DK, which has **not** yet been acquired.

## Rules

- Do not invent part numbers. Add manufacturer part numbers only once a part is actually selected.
- Quantities marked with a range (for example `2-4`) are planning estimates.
- Keep the CSV header exactly as defined; downstream tooling and the Hackster BOM table depend on it.
- Prices are not tracked in the preliminary BOM; add them to `final_bom.csv`.

## Current status

- Preliminary BOM created with all planned component categories.

## TODO

- [ ] Shortlist candidate parts for sensors (accelerometer, acoustic, temperature, RPM).
- [ ] Select the motor, driver, shaft, coupling, and bearing size as one consistent drive-train set.
- [ ] Add `final_bom.csv` with part numbers, suppliers, and prices once parts are confirmed.
- [ ] Update `Status` values as parts are confirmed and received.
