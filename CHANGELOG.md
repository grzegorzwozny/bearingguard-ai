# Changelog

All notable changes to BearingGuard AI will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project
intends to follow [Semantic Versioning](https://semver.org/spec/v2.0.0.html) once firmware releases
exist. Until then, entries describe documentation and planning milestones.

## [Unreleased]

### Added

- Initial repository scaffold for the BearingGuard AI concept:
  - Root documentation: README with project summary, architecture, condition levels, milestones,
    safety statement, limitations, and disclaimer; CONTRIBUTING; CODE_OF_CONDUCT; Apache-2.0 LICENSE.
  - Placeholder READMEs for every planned directory under `firmware/`, `hardware/`, `mechanical/`,
    `models/`, `tools/`, `datasets/`, `media/`, and `hackster/`, each describing purpose, expected
    files, planned implementation, current status, and TODO items.
  - Planning documents in `docs/`: architecture, project plan, test-rig plan, data-collection plan,
    Bluetooth service plan, Edge AI plan, safety, sustainability, and limitations.
  - `hardware/bom/preliminary_bom.csv` with all planned components (status: Planned, no part numbers).
  - `datasets/metadata/recording_metadata_template.csv` (header only).
  - `models/model_cards/bearing_anomaly_model.md` model card placeholder (model not yet trained).
  - `firmware/west.yml.example` example west manifest for an nRF Connect SDK workspace.
  - Hackster.io drafts: project story, hardware application answers, first project log, and
    attachments description.
  - GitHub issue templates (bug report, hardware test, feature request) and pull request template.
  - `.gitignore` and `.editorconfig`.

### Notes

- Project status: **concept and planning stage**. No hardware has been assembled, no data has been
  recorded, no firmware is functional, and no model has been trained.
- TODO: Add comparison links for `[Unreleased]` and future tags once the public repository URL exists.
