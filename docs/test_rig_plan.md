# Test Rig Plan

**Status: Draft - planned test rig.** The rig has not been designed in detail, built, or operated.
This document defines the concept and the requirements that the mechanical design in
[`../mechanical/`](../mechanical/README.md) must meet.

> **Rotating parts must never be operated without a suitable physical guard in place.** The guard and
> the emergency stop are mandatory components of the rig, not optional accessories. See
> [`safety.md`](safety.md).

## 1. Purpose of the rig

The rig exists to produce, repeatably and safely, a **healthy baseline** and a set of **controlled
deviation conditions** on a replaceable metal ball bearing, while the BearingGuard AI sensors measure
vibration, acoustic signal, housing temperature, and shaft speed at that bearing.

## 2. Layout concept

```text
                 +-------------+        +-----------+                   +----------------------+
  [PSU]--[E-STOP]| Motor driver|------->|   Motor   |==(flexible)==+    |  Instrumented support |
                 +-------------+        +-----------+   coupling   |    |  (test bearing B)     |
                                                                   |    |  accel / acoustic /   |
                                               +-------------+     |    |  housing temp         |
                                               | Support A   |=====+====|=======================|==[Adjustable load / brake]
                                               | (bearing A) |   shaft  |
                                               +-------------+     |    +----------------------+
                                                         [Imbalance disk]   [RPM sensor + magnet/marker]

  ===================================== rigid base plate =====================================
  [ transparent protective guard enclosing motor shaft, coupling, shaft, disk, supports, load ]
  [ RGB status LED and emergency stop visible / reachable from outside the guard               ]
```

## 3. Components

### 3.1 Motor

- Low-voltage DC or BLDC motor, chosen for quiet running, adequate torque for the load device, and a
  speed range covering the planned test speeds.
- Mounted on the base plate with a bracket that allows height alignment with the shaft.
- Powered through the emergency stop and a driver with a **hard maximum-speed limit**.

### 3.2 Flexible coupling

- Connects the motor shaft to the test shaft; tolerates small misalignment and isolates some motor
  vibration.
- The coupling's documented misalignment tolerance defines the upper bound of the misalignment test.
- Also serves as a possible location for the RPM magnet or marker.

### 3.3 Shaft

- Straight shaft with a diameter matching the bearing bore; length sufficient for two supports, the
  imbalance disk, and the load device.
- Checked for straightness and run-out before first use (values recorded).

### 3.4 Replaceable bearing supports

- Two supports (pillow blocks or housings) holding identical metal ball bearings.
- Support B is the **instrumented test position** and must offer a flat, machined surface for the
  accelerometer mount and a contact location for the housing temperature sensor.
- Bearings are exchangeable with simple tools so that several specimens (healthy and pre-worn) can be
  tested in independent runs; each specimen carries a `bearing_id`.

### 3.5 Adjustable load

- A radial and/or axial load device or a friction brake acting on the shaft near support B.
- Settings must be **indexed and repeatable** (for example numbered positions or a measured spring
  compression) so that `load_level` in the metadata is meaningful.
- Used for the "increased mechanical load" condition and to vary the operating point during baseline learning.

### 3.6 Imbalance disk

- A balanced disk on the shaft with threaded holes at known radii for **captive** test masses.
- Imbalance severity is set by mass and radius; the maximum permitted mass at the maximum speed is
  defined in the risk assessment and marked on the rig.
- Disk retention (set screw plus key or clamp) must be verified before each run.

### 3.7 RPM sensor

- Hall-effect sensor with a small magnet, or optical reflective sensor with a marker, mounted with a
  defined gap or distance to the shaft/coupling/disk.
- One pulse per revolution planned; sensor output wired to the DK for timer capture.

### 3.8 Sensor mounting positions

| Sensor | Planned position | Notes |
|---|---|---|
| Accelerometer | Support B housing, radial-vertical as primary orientation; axes documented | Stud or adhesive mount on a machined flat |
| Acoustic sensor | Microphone: fixed distance from support B, shielded from motor; piezo: on support B housing | Position name recorded in metadata |
| Housing temperature | Support B housing, as close to the outer race as possible | Thermal paste / clamp |
| Ambient temperature | On the base plate away from motor and bearings, shielded from direct airflow | Reference |
| RPM sensor | At coupling or disk | Gap set per sensor datasheet |

Position names follow the controlled vocabulary in
[`../mechanical/sensor_mounts/README.md`](../mechanical/sensor_mounts/README.md).

### 3.9 Base plate

- Rigid plate (metal or thick composite) carrying motor, supports, load device, sensors, and guard
  mounts; stiff enough that plate resonances are not dominant in the measurement band.
- Optional vibration-isolating feet to decouple from the bench.

### 3.10 Emergency stop

- Latching mushroom-head switch wired **directly in the motor power path**, independent of the DK,
  driver firmware, or Bluetooth.
- Reachable without reaching over or into the guard; tested before every session.

### 3.11 Transparent protective guard

- Rigid, transparent guard enclosing every rotating part with clearance; retained by tool-removable
  fasteners or an interlock that cuts motor power when opened.
- Must contain a released test mass at the controlled maximum speed (justified in the risk assessment).
- Cable pass-throughs via grommets; LED and e-stop visible/reachable from outside.
- Design in [`../mechanical/safety_guard/README.md`](../mechanical/safety_guard/README.md).

### 3.12 Controlled maximum speed

- A **documented, conservative maximum speed** is set in the motor driver (hardware limit where
  possible) and never exceeded, even for tests.
- The value depends on the bearing, disk mass, guard capability, and coupling; it is defined in the
  risk assessment (TODO) and marked on the rig.

## 4. Planned test conditions on the rig

| Condition | Method | Severity steps (preliminary) | Reset to healthy |
|---|---|---|---|
| Healthy baseline | New bearing, aligned, nominal torque, no test masses | none | - |
| Mechanical imbalance | Add captive masses to the disk | s1-s3 by mass and radius | Remove masses |
| Controlled misalignment | Shims under support A or coupling offset | s1-s3 by shim thickness | Remove shims, re-align |
| Loose bearing-housing mounting | Reduce support B fastener torque to defined values | s1-s3 by torque reduction | Re-torque to nominal |
| Increased mechanical load | Index the load device | s1-s3 by load setting | Release load |
| Pre-worn bearing | Install a specimen degraded by a documented procedure | by specimen | Install healthy specimen |

Every condition is run at several speeds within the limited range and in several independent runs.
Severity definitions are preliminary and will be fixed in the risk assessment and the data-collection plan.

## 5. Operating procedure (summary)

1. Execute the pre-run checklist (guard, e-stop test, speed limit, masses captive, torques, loose items).
2. Record metadata (bearing, condition, severity, load, positions, temperatures).
3. Start the motor at low speed; observe; ramp to the set-point.
4. Record the run; stop the motor; wait for standstill before any intervention.
5. De-energise (e-stop or switch) before opening the guard or touching the rig.

## 6. Current status

- Concept only. No part has been selected, designed, or built.

## TODO

- [ ] Choose bearing type/size and derive shaft, supports, coupling, and motor.
- [ ] Write the risk assessment and define the controlled maximum speed and maximum imbalance mass.
- [ ] Design the guard and the instrumented support surfaces.
- [ ] Define severity steps per condition with the data-collection plan.
- [ ] Write the full operating procedure and the pre-run checklist.
