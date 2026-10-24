# Diagrams (`media/diagrams`)

**Status: Placeholder** - no exported diagrams exist yet.

## Purpose

This directory holds **exported** images of diagrams for use where Mermaid cannot be rendered (Hackster
page, PDFs, presentations) and curated plots selected from the analysis and evaluation work. The
editable sources remain where they belong: Mermaid sources in [`../../hardware/block_diagrams/`](../../hardware/block_diagrams/README.md)
and in the `docs/` Markdown files; analysis scripts in `tools/`.

## Expected files

| File | Source | Planned content |
|---|---|---|
| `system_block_diagram.svg/.png` | `hardware/block_diagrams/system_block_diagram.mmd` | High-level system diagram |
| `electrical_block_diagram.svg/.png` | `hardware/block_diagrams/electrical_block_diagram.mmd` | Power domains, e-stop, interfaces |
| `edge_ai_pipeline.svg/.png` | `docs/edge_ai_plan.md` Mermaid | Processing flow |
| `ble_client_flow.svg/.png` | `docs/bluetooth_service_plan.md` Mermaid | Sequence diagram |
| `architecture_layers.svg/.png` | `docs/architecture.md` Mermaid | Layered view |
| `milestones.svg/.png` | `docs/project_plan.md` Mermaid | Milestone dependencies |
| `plots/*.png` | `tools/signal_analysis`, `models/evaluation` | Curated figures, each with the `recording_id`(s) and experiment ID in the file name or a sidecar caption |
| `diagrams_index.md` | - | Table of every exported file: source, export date, tool version |

## Rules

- Regenerate exports from sources; never edit exported images by hand.
- Plots must be reproducible from committed code plus referenced runs.
- Keep images web-sized.

## Current status

- Empty; sources exist only inline in Markdown.

## TODO

- [ ] Export the existing Mermaid diagrams with the Mermaid CLI and add `diagrams_index.md`.
- [ ] Add curated plots after the first analysis campaign.
