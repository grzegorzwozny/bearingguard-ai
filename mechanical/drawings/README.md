# Drawings (`mechanical/drawings`)

**Status: Placeholder** - no drawings exist yet.

## Purpose

This directory will contain 2D manufacturing and assembly drawings derived from the CAD models in
[`../cad/`](../cad/README.md): dimensions, tolerances, materials, and surface requirements for parts
that are machined, laser-cut, or 3D-printed, plus assembly and alignment drawings for the rig.

## Expected files

| File | Planned content |
|---|---|
| `base_plate.pdf` | Plate outline, thickness, mounting-hole pattern and tolerances |
| `instrumented_support_adapter.pdf` | Machined adapter or surface for the accelerometer stud/adhesive mount and the temperature-sensor contact point |
| `imbalance_disk.pdf` | Disk geometry, threaded holes for captive test masses, balance requirement, maximum mass per hole |
| `sensor_brackets.pdf` | Brackets for acoustic, ambient temperature, and RPM sensors |
| `guard_panels.pdf` | Guard panel dimensions, fastening points, cable pass-throughs |
| `rig_assembly_and_alignment.pdf` | Assembly order, coupling alignment procedure, shim positions for controlled misalignment, fastener torque values |
| `README.md` | This file with a drawing index (number, title, revision, status) |

## Information the drawings must contain

- Material and manufacturing method for each part.
- Dimensions and tolerances relevant to alignment and sensor coupling (flatness of the accelerometer surface).
- Fastener sizes and **torque values**, including the reduced torque used for the controlled
  "loose mounting" test condition and the normal torque used for the baseline.
- Shim thicknesses for each misalignment severity level.
- Clear marking of the maximum permitted imbalance mass and speed.

## Current status

- No drawings; depends on CAD and component selection.

## TODO

- [ ] Produce drawings for custom parts after the CAD assembly is reviewed.
- [ ] Define torque values and shim thicknesses in agreement with the test-rig plan.
- [ ] Maintain the drawing index with revision and status.
