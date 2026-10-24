# DSP and Feature Extraction (`firmware/dsp`)

**Status: Placeholder** - no DSP code exists yet.

## Purpose

This directory will contain the on-device signal processing that turns raw sensor samples into the
feature vector consumed by the Edge AI module: signal validation, filtering, windowing, and
time- and frequency-domain feature extraction. The same feature definitions will be implemented in
Python under [`../../tools/feature_extraction/`](../../tools/feature_extraction/README.md) so that
offline training and on-device inference use identical features.

## Expected files

| File | Planned content |
|---|---|
| `dsp_validate.c/.h` | Range checks, saturation and clipping detection, dropout / stuck-value detection, sensor-presence flags |
| `dsp_filter.c/.h` | DC removal, high-pass / band-pass filtering (IIR biquads), optional integration from acceleration to velocity for low-frequency features |
| `dsp_window.c/.h` | Fixed-length framing with overlap, Hann window for spectral features |
| `dsp_features_time.c/.h` | RMS, peak-to-peak, crest factor, kurtosis, impulse count above an adaptive threshold |
| `dsp_features_freq.c/.h` | FFT (CMSIS-DSP), spectral-band energies, dominant peak frequency and magnitude, optional order-normalised bands using RPM |
| `dsp_features_acoustic.c/.h` | Acoustic RMS and acoustic-band energies |
| `dsp_features_thermal.c/.h` | Temperature above ambient and temperature rise rate |
| `dsp_feature_vector.h` | Definition and ordering of the fused feature vector shared with `edge_ai/` and the host tooling |
| `Kconfig` | Window length, overlap, FFT size, band edges, feature-set selection |
| `CMakeLists.txt` | Adds the sources and links CMSIS-DSP |

## Planned feature set (preliminary)

| Group | Feature | Notes |
|---|---|---|
| Vibration (per axis and combined) | RMS | Overall vibration level |
| | Peak-to-peak acceleration | Impulsive content |
| | Crest factor | Peak / RMS; early defect indicator |
| | Kurtosis | Impulsiveness; sensitive to early surface damage |
| | Impulse count | Number of excursions above an adaptive threshold per window |
| | Spectral-band energy | Energy in several bands; band edges TODO after signal analysis |
| Acoustic | Acoustic RMS | Overall sound/contact energy |
| | Acoustic-band energy | Energy in selected bands |
| Thermal | Temperature above ambient | Housing minus ambient |
| | Temperature rise rate | Degrees per minute over a sliding window |
| Operating point | RPM | From the RPM driver |
| | Load level | If an adjustable-load sensor or setting is available; otherwise metadata only |

## Planned implementation notes

- Floating-point implementation first (the Cortex-M33 has an FPU); fixed-point only if profiling shows a need.
- Features are computed per window and then aggregated (mean / max over the evaluation period) before
  normalisation and inference.
- Feature definitions, units, and ordering are frozen in `dsp_feature_vector.h` and mirrored by the
  Python implementation; a cross-check test will compare both on identical input blocks.
- All DSP code will be host-testable with Ztest using synthetic signals (sine, impulses, noise) so that
  correctness does not depend on hardware availability.

## Current status

- No code exists; band edges, window lengths, and thresholds are undefined.

## TODO

- [ ] Define sample rates, window length, overlap, and FFT size.
- [ ] Define spectral bands after the first signal-analysis campaign.
- [ ] Implement the feature functions and host-side unit tests with synthetic signals.
- [ ] Add a Python/C equivalence test for the feature vector.
