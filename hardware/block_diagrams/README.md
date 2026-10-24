# Block Diagrams (`hardware/block_diagrams`)

**Status: Placeholder** - no diagram files have been exported yet.

## Purpose

This directory will contain the system-level and electrical block diagrams of BearingGuard AI in
editable form and as exported images for documentation and the Hackster project page.

## Expected files

| File | Planned content |
|---|---|
| `system_block_diagram.mmd` | Mermaid source of the high-level system diagram (sensors, DK, processing stages, BLE client, LED) - the same diagram as in the root README |
| `electrical_block_diagram.mmd` | Mermaid source of the electrical architecture: power domains, emergency stop in the motor power path, sensor interfaces to the DK |
| `signal_chain_block_diagram.mmd` | Per-channel signal chain: sensor -> analog front end (if any) -> interface -> driver -> DSP |
| `*.svg` / `*.png` | Exported images for use in `docs/`, `media/diagrams/`, and Hackster. Keep exports small; regenerate from the sources |

## Information the diagrams should contain

- Every sensor, its interface type (SPI, I2C, PDM, SAADC, GPIO), and the DK peripheral it uses.
- The separation of the motor power path from the sensing path, including the emergency stop.
- Power supply voltages for each domain.
- The RGB LED and its meaning per condition level.
- The BLE link and the planned client.

## Planned implementation

Diagrams are written in Mermaid so they can be reviewed as text and rendered by GitHub. Final
exports are produced with the Mermaid CLI and stored here and in
[`../../media/diagrams/`](../../media/diagrams/README.md).

## Current status

- The high-level diagram currently exists only inline in the root README and
  [`../README.md`](../README.md).

## TODO

- [ ] Move the inline Mermaid diagrams into `.mmd` source files here and reference them.
- [ ] Add the electrical block diagram after the power and emergency-stop concept is reviewed.
- [ ] Add the per-channel signal-chain diagram after sensor selection.
- [ ] Export SVG/PNG versions for documentation.
