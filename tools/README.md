# Tools

**Status: Planned** - no host-side tooling exists yet.

## Purpose

This directory will contain the host-side (PC) tooling that supports BearingGuard AI development:
capturing raw data from the device, analysing signals, extracting features identically to the firmware,
training and exporting models, and a Bluetooth LE dashboard for configuration and monitoring.

## Directory overview

| Directory | Content | Status |
|---|---|---|
| [`data_capture/`](data_capture/README.md) | Receive raw sample streams from the DK, write recordings with metadata | Placeholder |
| [`signal_analysis/`](signal_analysis/README.md) | Notebooks and scripts for exploring recordings: spectra, spectrograms, order analysis | Placeholder |
| [`feature_extraction/`](feature_extraction/README.md) | Python reference implementation of the firmware feature vector | Placeholder |
| [`model_training/`](model_training/README.md) | Training, evaluation, and export scripts | Placeholder |
| [`ble_dashboard/`](ble_dashboard/README.md) | BLE client application for live health display, trends, alerts, and configuration | Placeholder |

## Planned technology

- Python 3 with a pinned `requirements.txt` or `pyproject.toml` per tool (or one shared environment).
- NumPy / SciPy for analysis, Matplotlib for plots, a small ML framework for training, and a
  cross-platform BLE library for the dashboard.
- Command-line interfaces with arguments; no hard-coded paths.

## Rules

- Tools must read and write the metadata schema defined in
  [`../datasets/metadata/`](../datasets/metadata/README.md).
- Feature definitions must stay synchronised with `firmware/dsp/`; a cross-check test is planned.
- Tools must not write large outputs into the repository tree (use an external data directory passed
  as an argument).
- Follow [`../CONTRIBUTING.md`](../CONTRIBUTING.md) for style and license headers.

## Current status

- No code exists.

## TODO

- [ ] Decide on a single shared Python environment versus per-tool environments.
- [ ] Implement `data_capture` first; it gates every later step.
- [ ] Set up linting and formatting configuration (`ruff`, `black`).
