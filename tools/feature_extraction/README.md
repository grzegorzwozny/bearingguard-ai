# Feature Extraction (`tools/feature_extraction`)

**Status: Placeholder** - no feature code exists yet.

## Purpose

This directory will hold the **Python reference implementation** of the BearingGuard AI feature vector.
The firmware (`firmware/dsp/`) implements the same features in C for on-device inference; the Python
version is used for offline training and evaluation. Keeping both implementations numerically
equivalent is a hard requirement, otherwise models trained offline will behave differently on the device.

## Expected files

| File | Planned content |
|---|---|
| `bgai_features/__init__.py` | Package with a `FEATURE_VERSION` constant mirrored in the firmware |
| `bgai_features/validate.py` | Range, saturation, dropout checks matching `dsp_validate.c` |
| `bgai_features/filters.py` | DC removal and band filters with the same coefficients as the firmware |
| `bgai_features/windowing.py` | Framing and window function identical to `dsp_window.c` |
| `bgai_features/time_features.py` | RMS, peak-to-peak, crest factor, kurtosis, impulse count |
| `bgai_features/freq_features.py` | FFT, spectral-band energies, dominant peak, order-normalised bands using RPM |
| `bgai_features/acoustic_features.py` | Acoustic RMS and band energies |
| `bgai_features/thermal_features.py` | Temperature above ambient and rise rate |
| `bgai_features/vector.py` | Assembly of the fused feature vector in the canonical order |
| `extract.py` | Command-line tool: run directory in, per-window feature table (with run metadata columns) out |
| `tests/` | Unit tests with synthetic signals and a cross-check against C outputs exported from the firmware tests |
| `requirements.txt` | Pinned dependencies |

## Planned equivalence strategy

- The canonical feature order, units, window length, overlap, FFT size, and band edges are defined
  once (in a small JSON/YAML spec) and consumed by both implementations.
- Firmware unit tests dump feature outputs for fixture signals; the Python tests load the same fixtures
  and compare within a documented tolerance.
- `FEATURE_VERSION` is stored in every feature table and in every exported model parameter file.

## Current status

- Nothing implemented; feature definitions are preliminary (see `firmware/dsp/README.md`).

## TODO

- [ ] Write the feature specification file once signal analysis has fixed bands and windows.
- [ ] Implement the package and tests.
- [ ] Add the C/Python equivalence test to continuous integration.
