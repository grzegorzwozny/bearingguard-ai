# PCB (`hardware/pcb`)

**Status: Placeholder** - no PCB has been designed; a custom board may not be needed at all.

## Purpose

This directory is reserved for printed-circuit-board layout files if the project moves from breakout
boards and jumper wiring to a dedicated **sensor carrier board**. Such a board would plug onto the
nRF54LM20 DK headers (or sit at the bearing and connect via a short cable) and host the accelerometer,
acoustic sensor or front end, temperature sensors, RPM sensor connector, and RGB LED.

## Expected files (only if a custom board is designed)

| File | Planned content |
|---|---|
| `sensor_carrier.kicad_pro` / `.kicad_pcb` | KiCad project and layout |
| `fabrication/` | Gerber and drill files, assembly drawings, pick-and-place files for the final reviewed revision |
| `renders/` | Small PNG renders of top and bottom views |
| `DESIGN_NOTES.md` | Stack-up, mechanical outline and mounting holes, keep-out areas, analog/digital partitioning, grounding, connector choices |

## Design considerations

- The accelerometer should be mounted rigidly to the bearing housing, not on a board hanging off the DK.
  A carrier board at the bearing with a short cable to the DK is therefore more likely than a shield.
- The board outline and mounting holes must match the sensor-mount design in
  [`../../mechanical/sensor_mounts/README.md`](../../mechanical/sensor_mounts/README.md).
- Separate analog (piezo, NTC) and digital (SPI, PDM) areas; provide a solid ground reference.
- Choose connectors that cannot be mis-mated and that tolerate vibration.

## Current status

- No decision has been made on a custom board. The first iteration will use breakout boards.

## TODO

- [ ] Decide after bring-up whether breakout wiring is adequate or a carrier board is justified.
- [ ] If a board is designed, document the outline requirements with the mechanical team first.
