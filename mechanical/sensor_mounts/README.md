# Sensor Mounts (`mechanical/sensor_mounts`)

**Status: Placeholder** - no mount has been designed.

## Purpose

This directory will contain the design of the mechanical interfaces between the sensors and the test
rig. For vibration measurement in particular, the mount determines the usable frequency range and the
repeatability of the data far more than the sensor's electrical specification does. Consistent,
documented sensor positions are also a requirement of the dataset metadata
(`accelerometer_position`, `acoustic_sensor_position`).

## Expected files

| File | Planned content |
|---|---|
| `accelerometer_mount.md` | Mounting method (stud, adhesive, or magnetic for comparison), surface preparation, orientation of the X/Y/Z axes relative to radial-horizontal, radial-vertical, and axial directions, expected mounted resonance considerations |
| `acoustic_sensor_mount.md` | Microphone position and distance from the bearing, windscreen/shield from motor noise; or piezo contact sensor coupling (adhesive/clamp, coupling medium) |
| `temperature_sensor_mount.md` | Housing-sensor contact method (thermal paste, clamp), insulation from airflow, ambient-sensor position |
| `rpm_sensor_mount.md` | Hall-sensor or optical-sensor holder, air gap or sensing distance, magnet/marker fixing and balancing |
| `position_naming.md` | Controlled vocabulary for sensor positions used in the metadata, e.g. `support_B_radial_vertical` |
| `cad/` (reference) | Models live in [`../cad/`](../cad/README.md) |

## Design principles

- **Stiff and direct**: the accelerometer is mounted directly on the instrumented bearing support on a
  flat, clean surface; no long brackets.
- **Repeatable**: the same position and orientation for every run; marked on the rig and recorded in
  the metadata.
- **Documented alternatives**: if different positions are compared during signal analysis, each gets its
  own name in `position_naming.md`.
- **Safe**: no mount may protrude into the path of rotating parts or interfere with the guard.

## Current status

- No design. Depends on the choice of bearing support and sensor packages.

## TODO

- [ ] Define the position vocabulary before the first recording campaign.
- [ ] Design the accelerometer mount for the selected support; specify surface flatness.
- [ ] Define acoustic, temperature, and RPM sensor mounts.
- [ ] Verify mounts against guard clearance in CAD.
