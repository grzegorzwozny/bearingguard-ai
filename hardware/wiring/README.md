# Wiring (`hardware/wiring`)

**Status: Placeholder** - no wiring has been defined.

## Purpose

This directory will document how the sensors, RPM sensor, RGB LED, power, and emergency stop are
physically connected: pin-to-pin wiring tables, connector pinouts, cable types and lengths, routing
on the rig, and grounding and shielding practice. It is the electrical counterpart of the devicetree
overlays in [`../../firmware/boards/`](../../firmware/boards/README.md); the two must always agree.

## Expected files

| File | Planned content |
|---|---|
| `wiring_table.csv` | One row per connection: `signal, from_device, from_pin, to_device, to_pin, cable_type, length_cm, notes` |
| `connector_pinouts.md` | Pinout of every connector used on sensor cables and the carrier board (if any) |
| `cable_routing.md` | Where cables run on the rig, strain relief, keep-away from the motor and rotating parts, guard pass-throughs |
| `grounding_and_shielding.md` | Single-point grounding, shield termination, separation of motor-domain and sensing-domain wiring |
| `power_distribution.md` | Supply voltages, current budget per consumer, fusing, emergency-stop placement in the motor path |
| `photos/` (reference) | Photos of the finished wiring belong in [`../../media/photos/`](../../media/photos/README.md) |

## Information the wiring documentation must contain

- The DK I/O voltage and each sensor's supply and logic voltage.
- Pull-up/pull-down requirements (I2C lines, open-collector RPM sensor output).
- Cable shielding and twisted-pair use for SPI/PDM and analog lines.
- Clear statement that the emergency stop interrupts motor power directly and does not depend on the DK.
- Cable entry through the protective guard without creating pinch points.

## Current status

- No wiring exists. Pin assignments are `TODO` in `firmware/boards/README.md`.

## TODO

- [ ] Create `wiring_table.csv` once sensors and DK pins are chosen.
- [ ] Define the power-distribution concept and current budget.
- [ ] Write the grounding and shielding guidance before the first recordings.
- [ ] Verify the wiring table against the devicetree overlay before flashing.
