# Video (`media/video`)

**Status: Placeholder** - no video exists.

## Purpose

Short videos will demonstrate the rig in operation, the LED condition indication, and the BLE dashboard
responding to controlled conditions. They are important for the Hackster project page and for showing
the safety setup (guard, emergency stop) in practice.

## Policy

**Video files are not committed to this repository** (`.gitignore` excludes common video formats).
Videos are hosted on a video platform or project storage and **linked** from the files in this directory.

## Expected files

| File | Planned content |
|---|---|
| `video_index.md` | Table: title, hosted URL, duration, date, what it shows, rig configuration, related `recording_id`s, safety note |
| `scripts/<title>_script.md` | Shot list and narration script for each planned video |
| `thumbnails/*.jpg` | Small thumbnails for embedding in Markdown |

## Planned videos

| Title | Content | Milestone |
|---|---|---|
| Concept overview | Narrated walk-through of the architecture diagrams (can be produced before hardware exists; must be labelled as concept) | M0-M1 |
| Rig and safety | Guard, e-stop test, speed limit, pre-run checklist in practice | M2 |
| Bring-up | Sensors streaming to the capture tool | M3-M4 |
| Baseline learning and monitoring | LED and dashboard during baseline learning and healthy monitoring | M8-M9 |
| Controlled conditions | Dashboard response to imbalance, misalignment, loose mounting, load, pre-worn bearing (with honest commentary on what is and is not detected) | M10 |

## Rules

- Every video showing the rig running must show the guard fitted; videos must never show unsafe operation.
- No claims in narration that are not supported by documented results.
- No people identifiable without consent.

## Current status

- No videos; no scripts.

## TODO

- [ ] Write the concept-overview script.
- [ ] Create `video_index.md` when the first video is published.
