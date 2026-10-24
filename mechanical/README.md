# Mechanical

**Status: Planned** - no mechanical parts have been designed, manufactured, or assembled.

## Purpose

This directory documents the mechanical side of BearingGuard AI: the bench-top test rig on which
healthy and degraded bearing conditions are produced, the sensor mounts that couple the sensors to the
bearing housing, and the protective guard that makes operating the rig safe. The detailed plan is in
[`../docs/test_rig_plan.md`](../docs/test_rig_plan.md); safety requirements are in
[`../docs/safety.md`](../docs/safety.md).

## Directory overview

| Directory | Content | Status |
|---|---|---|
| [`cad/`](cad/README.md) | 3D CAD models of the rig, brackets, guard, and custom parts (native format plus STEP/STL) | Placeholder |
| [`drawings/`](drawings/README.md) | 2D drawings with dimensions and tolerances for manufactured or machined parts | Placeholder |
| [`sensor_mounts/`](sensor_mounts/README.md) | Mounting design for accelerometer, acoustic sensor, temperature sensors, RPM sensor | Placeholder |
| [`safety_guard/`](safety_guard/README.md) | Transparent protective guard design, fastening/interlock concept, cable pass-throughs | Placeholder |

## Planned rig concept

```text
 [Motor] --(flexible coupling)-- [Bearing support A] ==== shaft ==== [Bearing support B (instrumented)]
                                                      |                       |
                                               [Imbalance disk]        [Adjustable load / brake]
                                                                       [Accelerometer, acoustic,
                                                                        temperature sensors]
 [RPM sensor + magnet/marker on shaft]        all mounted on a rigid base plate
 [Emergency stop]  [Transparent guard over every rotating part]
```

Key mechanical planning decisions:

- **Rigid base plate** to limit plate resonances inside the measurement band.
- **Instrumented bearing support** with a flat, machined surface for a stud- or adhesive-mounted
  accelerometer and a thermal-contact location for the housing temperature sensor.
- **Quick bearing exchange** so that multiple bearing specimens can be tested in independent runs.
- **Controlled fault injection**: captive imbalance masses, shim-based misalignment, torque-limited
  "loose mounting", indexed load setting.
- **Guard first**: the rig is not operated, even briefly, without the guard fitted.

## Current status

- Concept only; no CAD exists; no parts have been chosen.

## TODO

- [ ] Define bearing size, shaft diameter, and support type as one consistent set (with the BOM).
- [ ] Produce the base-plate layout and the guard envelope in CAD.
- [ ] Design sensor mounts for the instrumented support.
- [ ] Carry out and document a risk assessment before first operation.
