# Safety Guard (`mechanical/safety_guard`)

**Status: Placeholder** - no guard has been designed. **The rig must not be operated without one.**

## Purpose

This directory will contain the design of the transparent protective guard that encloses every
rotating part of the BearingGuard AI test rig (motor shaft, coupling, shaft, bearing supports,
imbalance disk, load device) while allowing observation, sensor cabling, and LED visibility.
The guard is a mandatory part of the rig, not an accessory. The overall safety requirements are in
[`../../docs/safety.md`](../../docs/safety.md).

## Expected files

| File | Planned content |
|---|---|
| `guard_requirements.md` | Protected zone, minimum clearances, material and thickness rationale, containment of a released test mass at maximum speed, fastening/interlock concept, access for bearing exchange, cable and sensor pass-throughs, ventilation |
| `guard_design.md` | Chosen geometry, panels, fasteners, hinge/removal method, interlock or captive-fastener solution, labelling |
| `risk_assessment.md` | Hazard list (entanglement, ejected parts, hot surfaces, electrical, noise), severity/likelihood estimate, mitigations, residual risk, sign-off before first operation |
| `pre_run_checklist.md` | Checklist executed before every session: guard fitted and secured, emergency stop tested, speed limit set, masses captive, fasteners at specified torque, loose items removed |
| CAD and drawings | In [`../cad/`](../cad/README.md) and [`../drawings/`](../drawings/README.md) |

## Requirements the design must satisfy (preliminary)

- Covers all rotating parts; no reach-in path to a rotating element when fitted.
- Transparent, rigid material of sufficient thickness to contain a released imbalance mass at the
  controlled maximum speed (justified in the risk assessment).
- Cannot be removed without tools, or is interlocked so that motor power is removed when opened.
- Sensor cables pass through grommets or slots that do not create pinch points.
- The RGB status LED and the emergency stop remain visible and reachable from outside the guard.
- Allows bearing exchange and shim/mass changes only with the motor de-energised.

## Current status

- Requirements drafted at the concept level only; no design or risk assessment exists.

## TODO

- [ ] Write `guard_requirements.md` and `risk_assessment.md` before any mechanical procurement.
- [ ] Design the guard in CAD together with the base plate.
- [ ] Decide between tool-removable fasteners and an electrical interlock.
- [ ] Write and adopt the pre-run checklist.
