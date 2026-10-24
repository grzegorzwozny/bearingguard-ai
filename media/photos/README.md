# Photos (`media/photos`)

**Status: Placeholder** - no photographs exist because no hardware exists.

## Purpose

Photographs documenting the physical build: the test rig at each stage, sensor mounting details, the
nRF54LM20 DK wiring, the guard and emergency stop, and screenshots of the dashboard. Photos support the
documentation, the Hackster story, and reproducibility (someone else should be able to see how a sensor
was mounted).

## Expected files

| File pattern | Planned content |
|---|---|
| `rig/<stage>_<description>.jpg` | Rig build stages: base plate, supports, motor, coupling, disk, load device, guard |
| `sensors/<sensor>_<position>.jpg` | Close-ups of each sensor mount with the position name from the controlled vocabulary |
| `electronics/<description>.jpg` | DK wiring, breakout boards, connectors, LED, e-stop wiring |
| `dashboard/<view>.png` | Screenshots of the BLE dashboard views |
| `photos_index.md` | Table: file, date, what it shows, status (build stage), related `recording_id` or milestone |

## Rules

- Resize for web (preliminary limit: a few hundred kilobytes each); originals stay outside the repository.
- No people without consent; no personal data visible.
- Captions must be honest about status (mock-up, partial build, final build).
- Photos of safety-relevant details (guard fitted, e-stop) are encouraged for every campaign.

## Current status

- Empty.

## TODO

- [ ] Start `photos_index.md` with the first build photos (milestone M2).
- [ ] Add sensor-mount photos for every position used in recordings.
