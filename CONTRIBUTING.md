# Contributing to BearingGuard AI

Thank you for your interest in BearingGuard AI. The project is currently at the **concept and planning
stage**, so the most valuable contributions right now are reviews of the planning documents, sensor and
component suggestions, test-rig safety feedback, and improvements to the proposed firmware, data, and
Edge AI architecture.

Please also read the [Code of Conduct](CODE_OF_CONDUCT.md).

## Ways to contribute

| Area | Examples |
|---|---|
| Documentation | Clarify or correct planning documents in `docs/`, improve placeholder READMEs, fix typos |
| Hardware | Suggest sensors, mounting approaches, or wiring practices; review the preliminary BOM |
| Mechanical and safety | Review the test-rig plan, guard design, emergency-stop concept, and speed limits |
| Firmware (later) | Zephyr/nRF Connect SDK drivers, DSP, BLE service, Edge AI integration, tests |
| Data and models (later) | Capture tooling, feature extraction, model training and evaluation scripts |
| Dashboard (later) | BLE client for configuration, trends, and alerts |

Before starting substantial work, open an issue using one of the templates in
[`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE/) so the scope can be discussed.

## Ground rules

1. **No unsupported claims.** Do not describe hardware, firmware, measurements, test results, or model
   performance as completed unless they really are and the evidence is in the repository. Use the
   markers `Status: Planned`, `Status: Placeholder`, and `TODO` for incomplete work.
2. **No fabricated data.** Never commit invented measurement data, test results, or metadata rows.
3. **No large binaries.** Do not commit raw recordings, raw audio, trained models, build outputs, IDE
   caches, or large images and videos. Store them externally and reference them in documentation.
   See [`.gitignore`](.gitignore) and [`datasets/README.md`](datasets/README.md).
4. **No secrets.** Never commit credentials, private keys, API tokens, `.env` files, or personal data.
5. **No third-party copyrighted material.** Do not commit copied datasheets, schematics, images, or
   text. Link to official sources instead (see [`hardware/datasheets/README.md`](hardware/datasheets/README.md)).
6. **Safety first.** Proposals that remove or weaken guarding, emergency stop, or speed limiting on the
   test rig will not be accepted. See [`docs/safety.md`](docs/safety.md).
7. **English only** in documentation, code comments, commit messages, and identifiers.

## Workflow

1. Fork the repository and create a branch from the default branch:
   - `docs/<topic>` for documentation changes
   - `feat/<topic>` for new functionality
   - `fix/<topic>` for bug fixes
   - `hw/<topic>` and `mech/<topic>` for hardware and mechanical changes
2. Make focused commits using the [Conventional Commits](https://www.conventionalcommits.org/) style:
   - `docs: describe sensor mounting positions`
   - `feat(firmware): add accelerometer driver skeleton`
   - `fix(tools): handle missing metadata column`
3. Make sure every new file has meaningful content (no empty placeholders) and that Markdown links
   resolve.
4. Open a pull request using the [pull request template](.github/pull_request_template.md) and
   describe what was changed, why, and how it was verified.

## Coding conventions (for future source code)

Source code is not part of the repository yet. When it is added, the following conventions apply.

### Firmware (C, Zephyr / nRF Connect SDK)

- Follow the [Zephyr coding style](https://docs.zephyrproject.org/latest/contribute/style/index.html)
  (tabs, 100-column limit, `snake_case`), enforced with `clang-format` using Zephyr's configuration.
- Prefer Zephyr subsystems and APIs (sensor API, Bluetooth host, settings, logging) over ad-hoc code.
- Keep board-specific configuration in devicetree overlays and Kconfig fragments under `firmware/boards/`.
- Add unit tests (Ztest / Twister) for DSP and feature-extraction code under `firmware/tests/`.
- Do not commit generated build directories.

### Host tooling (Python)

- Target a current Python 3 release; pin dependencies in a `requirements.txt` or `pyproject.toml`.
- Follow PEP 8; format with `black` or `ruff format`; lint with `ruff`.
- Scripts must read configuration from arguments or environment variables, never from hard-coded
  absolute paths.

### Hardware and mechanical files

- Prefer open formats (KiCad for schematics and PCB, STEP and STL for mechanical parts) alongside
  any native CAD format.
- Keep rendered PDFs or PNGs of schematics and drawings small and only for the final reviewed revision.

## License and copyright notices

By contributing you agree that your contributions are licensed under the
[Apache License, Version 2.0](LICENSE), the same license that covers the project
(inbound = outbound).

Every **source file** (C, C++, Python, CMake, Kconfig, devicetree, shell scripts) must start with a
short notice using an SPDX identifier. **Do not** add license headers to Markdown files or CSV templates.

C / C++ / devicetree:

```c
/*
 * Copyright (c) 2026 BearingGuard AI contributors
 *
 * SPDX-License-Identifier: Apache-2.0
 */
```

Python / CMake / Kconfig / shell / YAML:

```python
# Copyright (c) 2026 BearingGuard AI contributors
# SPDX-License-Identifier: Apache-2.0
```

> TODO: Confirm the exact copyright-holder wording before the first source files are committed.

## Reporting hardware test observations

Once hardware exists, use the **Hardware test** issue template to report observations from the test
rig. Include rig configuration, safety checks performed, sensor positions, and the run identifier, and
attach plots or summaries rather than raw recordings.

## Questions

Open a discussion or an issue. Please do not send security- or safety-related reports as public issues
if they could put someone at risk; mark them clearly and the maintainers will follow up.

> TODO: Add a maintainer contact address once the project has a public contact point.
