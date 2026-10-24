# Schematics (`hardware/schematics`)

**Status: Placeholder** - no schematics exist yet.

## Purpose

This directory will contain schematics for any custom electronics in the project. In the first
iteration the nRF54LM20 DK is wired to sensor breakout boards, so custom circuitry is expected to be
limited to small interface and front-end circuits. Everything here must be the project's own work;
copied proprietary schematics are not permitted.

## Expected files

| File | Planned content |
|---|---|
| `sensor_interface.kicad_sch` | Interconnection of DK header pins, sensor breakouts, pull-ups, decoupling, and connectors |
| `piezo_front_end.kicad_sch` | Only if the piezoelectric contact sensor is chosen: charge or voltage amplifier, biasing to mid-scale, anti-alias filtering, clamping for the SAADC input |
| `ntc_divider.kicad_sch` | Only if NTC thermistors are chosen: voltage dividers and filtering for the SAADC |
| `rpm_sensor_interface.kicad_sch` | Pull-up / level conditioning for a Hall-effect or optical sensor output; input protection |
| `status_led.kicad_sch` | RGB LED driver (series resistors or small transistor stage) connected to PWM outputs |
| `estop_status_input.kicad_sch` | Optional isolated input so the DK can *monitor* (never control) the emergency-stop state |
| `*.pdf` | Exported PDF of the final reviewed revision only |
| `README.md` | This file, with a revision table once schematics exist |

## Design rules and considerations

- Confirm the DK I/O voltage and the sensor supply/logic levels; add level shifting only if required.
- Keep analog front ends physically close to the sensor and the SAADC input short and shielded.
- Every circuit that connects to the motor domain must be galvanically isolated or avoided.
- Document each schematic sheet with purpose, interface, and review status.

## Current status

- No circuits have been designed. Sensor types are not yet decided, so the required front ends are unknown.

## TODO

- [ ] Decide on sensor types (see `firmware/drivers/*/README.md`) to determine which sheets are needed.
- [ ] Draft `sensor_interface.kicad_sch` with the DK header pin assignment from `firmware/boards/`.
- [ ] Design and review any analog front end; record review notes here.
- [ ] Export a PDF of the reviewed revision and reference it from the Hackster attachments description.
