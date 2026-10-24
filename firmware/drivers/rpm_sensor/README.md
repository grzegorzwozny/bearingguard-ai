# RPM Sensor Driver (`firmware/drivers/rpm_sensor`)

**Status: Placeholder** - no driver code exists yet.

## Purpose

This directory will contain the shaft-speed measurement. Rotational speed is essential for:

- normalising vibration and acoustic features against the operating point,
- computing speed-related spectral features (shaft order and, later, bearing characteristic frequencies),
- detecting that the machine is stopped or running outside the learned speed range.

Two sensor options are planned: a **Hall-effect sensor** with a small magnet on the shaft or coupling,
or an **optical reflective sensor** with a reflective or dark marker on the shaft or disk.

## Expected files

| File | Planned content |
|---|---|
| `rpm.h` | API: `rpm_init()`, `rpm_get_rpm()`, `rpm_get_period_us()`, `rpm_is_rotating()`, pulses-per-revolution configuration |
| `rpm_capture.c` | Pulse timing using GPIOTE events connected to a TIMER capture channel through DPPI, so pulse timestamps do not depend on interrupt latency; fallback GPIO interrupt implementation |
| `rpm_filter.c` | Debouncing / glitch rejection, period averaging over a configurable number of pulses, stall timeout |
| `Kconfig` | `CONFIG_BGAI_RPM_PULSES_PER_REV`, `CONFIG_BGAI_RPM_STALL_TIMEOUT_MS`, `CONFIG_BGAI_RPM_AVG_PULSES` |
| `CMakeLists.txt` | Adds the sources to the build |

## Planned requirements

| Requirement | Preliminary target | Rationale |
|---|---|---|
| Speed range | From standstill to the rig's controlled maximum speed | Must detect "stopped" reliably |
| Resolution | Better than 1 % at nominal speed (TODO) | Adequate for normalisation and order tracking |
| Pulses per revolution | 1 (single magnet or marker); configurable | Simplicity; more markers improve low-speed update rate |
| Latency | One to a few revolutions | Normalisation does not need instantaneous speed |

## Planned implementation notes

- Pulse-to-pulse periods are measured with a hardware timer; RPM is derived as
  `60 * 1e6 / (period_us * pulses_per_rev)`.
- A stall timeout declares `rpm = 0` when no pulse arrives within the configured interval, which also
  gates health evaluation (no evaluation while stopped).
- The RPM value is attached to every feature vector so that offline analysis and on-device
  normalisation use the same operating-point information.
- Mechanical details (magnet fixing, sensor gap, marker contrast) belong in
  [`../../../mechanical/sensor_mounts/README.md`](../../../mechanical/sensor_mounts/README.md).

## Current status

- Sensor type not yet selected; no code written.
- Availability of GPIOTE/TIMER/DPPI resources on the chosen board target is to be confirmed.

## TODO

- [ ] Choose Hall-effect or optical sensing and document mounting constraints.
- [ ] Verify timer-capture resources in the pinned SDK release.
- [ ] Define averaging and stall-timeout values for the planned speed range.
- [ ] Implement the driver and a host-side unit test for the period-to-RPM and stall logic.
