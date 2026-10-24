# Hackster.io Materials

**Status: Drafts** - publication-ready drafts for a Hackster.io project at the concept stage. Nothing
in these files claims completed hardware, measurements, firmware, or model results.

## Purpose

This directory holds the text and supporting descriptions for the BearingGuard AI Hackster.io project
page and any hardware-application form: the project story, the application answers, project logs, and
the description of which repository files will be linked as attachments.

## Files

| File | Content | Status |
|---|---|---|
| [`project_story.md`](project_story.md) | Publication-ready draft of the Hackster project story (introduction, problem, solution, architecture, diagram, BOM, DK/Edge AI/BLE usage, test rig, data plan, milestones, sustainability, limitations, planned attachments) | Draft |
| [`hardware_application.md`](hardware_application.md) | Clearly separated draft answers for a hardware-application form | Draft; personal background is a TODO placeholder |
| [`project_log_01.md`](project_log_01.md) | First project log: concept, planning, and repository scaffold | Draft |
| [`attachments_description.md`](attachments_description.md) | Which future files will be linked or uploaded under Code, Schematics, and CAD attachments | Draft |

## Publication rules

- Copy text from these files to Hackster only after a review for unsupported claims; the project
  status must be stated clearly at the top of the story.
- Diagrams are exported from the Mermaid sources into `media/diagrams/` for upload, because Hackster
  does not render Mermaid.
- Images and videos follow the rules in [`../media/README.md`](../media/README.md).
- Never publish personal data of third parties or anything that could be read as a safety endorsement.
- Keep the Hackster page and the repository consistent: update the log here first, then publish.

## Planned additional logs

| Log | Trigger |
|---|---|
| `project_log_02.md` | Hardware acquired; first look at the nRF54LM20 DK and sensors |
| `project_log_03.md` | Rig built and safety review completed |
| `project_log_04.md` | Firmware bring-up and first recordings |
| `project_log_05.md` | Signal analysis findings and feature design |
| `project_log_06.md` | Controlled fault campaigns |
| `project_log_07.md` | Model training and evaluation results (honest) |
| `project_log_08.md` | On-device pipeline, BLE service, dashboard |
| `project_log_09.md` | Final demonstration and lessons learned |

## TODO

- [ ] Replace the personal-background placeholder in `hardware_application.md` before submission.
- [ ] Export diagrams for upload.
- [ ] Review all drafts for unsupported claims before publishing.
