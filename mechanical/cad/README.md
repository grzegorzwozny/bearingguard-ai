# CAD Models (`mechanical/cad`)

**Status: Placeholder** - no CAD models exist yet.

## Purpose

This directory will contain the 3D CAD models of the BearingGuard AI test rig and all custom parts:
base-plate layout, bearing-support positions, motor mount, imbalance disk, load device bracket, sensor
brackets, RPM-sensor holder, LED holder, and the transparent protective guard.

## Expected files

| File | Planned content |
|---|---|
| `rig_assembly.<native>` | Full rig assembly in the chosen CAD tool's native format (FreeCAD `.FCStd` preferred for open collaboration) |
| `rig_assembly.step` | Neutral STEP export of the assembly for review without the native tool |
| `parts/*.step`, `parts/*.stl` | Individual custom parts: STEP for machining/reference, STL for 3D printing |
| `parts/README.md` | Table of custom parts: name, function, material, manufacturing method, quantity, drawing reference |
| `renders/*.png` | Small rendered images for documentation and Hackster |

Native files of large commercial CAD tools may be committed if they are the project's own work, but
always provide STEP/STL alongside them. Temporary and backup CAD files are ignored by `.gitignore`.

## Information the models must capture

- Shaft centre height and bearing-support spacing.
- Clearance for the imbalance disk and its masses at maximum speed.
- Flat, machined sensor mounting surfaces on the instrumented support.
- Guard envelope covering the motor shaft, coupling, shaft, disk, and load device, with clearance.
- Cable routes and guard pass-throughs.
- Mounting-hole pattern on the base plate.

## Current status

- No CAD files. Bearing size and shaft diameter are not yet selected.

## TODO

- [ ] Choose the CAD tool and record the version used.
- [ ] Model the base plate, supports, motor, coupling, shaft, and disk at the selected dimensions.
- [ ] Add sensor mounts and the guard; check clearances.
- [ ] Export STEP/STL and renders; list parts in `parts/README.md`.
