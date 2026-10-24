# Safety

**Status: Draft.** These requirements apply to the planned test rig and to the role of the BearingGuard
AI device. They must be reviewed and adopted before any mechanical procurement or operation. A formal
risk assessment is required (TODO) and will be stored in
[`../mechanical/safety_guard/`](../mechanical/safety_guard/README.md).

## 1. What BearingGuard AI is - and is not

BearingGuard AI is an **experimental, advisory predictive-maintenance demonstrator**. It observes a
bearing and reports a health score, a condition level, and a recommendation to a human.

It is **not**:

- certified industrial protection or condition-monitoring equipment,
- an emergency shutdown, interlock, or safety-related control system,
- a replacement for machine guarding, lock-out procedures, or qualified inspection,
- connected in any way to the control of the test-rig motor.

Nothing received or computed by the device, and nothing sent over Bluetooth, can start, stop, speed up,
or slow down the rig. Motor control and emergency stop are entirely independent of the device.

## 2. Hazards of the planned test rig

| Hazard | Source | Possible harm |
|---|---|---|
| Entanglement / contact with rotating parts | Shaft, coupling, disk, exposed bearing | Injury to hands, hair, clothing |
| Ejected parts | Test masses, set screws, failed disk or coupling, bearing fragments | Eye and body injury |
| Loose-mounting tests | Deliberately reduced fastener torque | Component walk-off, vibration escalation |
| Imbalance tests | Added masses | Elevated vibration, fastener loosening, ejection |
| Hot surfaces | Bearing housing under load, motor | Burns |
| Electrical | Motor supply, driver, wiring | Shock, fire |
| Noise | Motor, bearings under fault conditions | Hearing damage over time |
| Stored energy | Rotating inertia after power removal | Contact injury during run-down |

## 3. Mandatory requirements

1. **Guard.** Rotating parts must **never** be operated without a suitable, rigid, transparent physical
   guard enclosing every rotating element. The guard is retained by tool-removable fasteners or an
   interlock that removes motor power when opened. See
   [`../mechanical/safety_guard/README.md`](../mechanical/safety_guard/README.md).
2. **Emergency stop.** A latching emergency stop that removes motor power directly, independent of the
   DK, driver firmware, or Bluetooth, must be installed, reachable without reaching into the guard, and
   tested before every session.
3. **Controlled maximum speed.** A documented, conservative maximum speed is set in the motor driver
   (hardware limit where possible) and never exceeded. The value is defined in the risk assessment.
4. **Bounded fault injection.** Maximum imbalance mass, minimum fastener torque for loose-mounting
   tests, maximum shim thickness for misalignment, and maximum load are defined in the risk assessment,
   marked on the rig, and never exceeded. Test masses must be captive.
5. **Standstill before intervention.** Wait for complete standstill and de-energise before opening the
   guard or touching any part of the rig.
6. **Personal protective equipment.** Eye protection is mandatory; hearing protection when the rig
   runs; no loose clothing, jewellery, or unsecured long hair.
7. **Pre-run checklist.** Executed and recorded before every session (guard fitted and secured, e-stop
   tested, speed limit confirmed, masses captive, fasteners at specified torque, loose items removed,
   cables secured).
8. **Two-person rule for fault tests.** Imbalance, loose-mounting, and pre-worn-bearing runs are not
   performed alone.
9. **Electrical safety.** Low-voltage motor supply with appropriate fusing; sensing domain isolated from
   the motor domain; no exposed conductors.
10. **Thermal.** Housing temperature is monitored; runs are stopped if the housing exceeds a defined
    limit (TODO) regardless of the device's health score.

## 4. Safety-related documents (planned)

| Document | Location | Status |
|---|---|---|
| Risk assessment | `mechanical/safety_guard/risk_assessment.md` | TODO |
| Guard requirements and design | `mechanical/safety_guard/` | TODO |
| Pre-run checklist | `mechanical/safety_guard/pre_run_checklist.md` | TODO |
| Operating procedure | `docs/test_rig_plan.md` (summary), full procedure TODO | Draft |
| Hardware test reports | GitHub issues using the Hardware test template | Template exists |

## 5. Software and data safety notes

- The firmware's `FAULT` state and Device Status flags inform the operator of device problems; they
  have no effect on the rig.
- Health scores and recommendations are advisory and may be wrong (see
  [`limitations.md`](limitations.md)); operators must not rely on them for personal safety decisions.
- Raw audio capture is minimised to protect privacy (see
  [`../datasets/README.md`](../datasets/README.md)).

## 6. Incident handling

Any incident or near miss stops work until the cause is understood and the risk assessment is updated.
Record it in a GitHub issue (Hardware test template, marked `safety`) without personal data.

## TODO

- [ ] Write and sign off the risk assessment before procurement of rotating parts.
- [ ] Define the controlled maximum speed, maximum imbalance mass, torque limits, shim limits, load limit, and housing temperature limit.
- [ ] Write the pre-run checklist and the full operating procedure.
