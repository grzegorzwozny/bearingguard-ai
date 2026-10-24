# Signal Analysis (`tools/signal_analysis`)

**Status: Placeholder** - no analysis has been performed; no recordings exist.

## Purpose

This directory will contain notebooks and scripts for exploring recorded data before features and
models are designed: inspecting raw waveforms, spectra, spectrograms, order spectra, envelope spectra,
and thermal trends across runs and conditions. The outcome of this phase drives the choice of sample
rates, window lengths, spectral bands, and the feature set.

## Expected files

| File | Planned content |
|---|---|
| `notebooks/01_waveform_overview.ipynb` | Load a run, plot time series per channel, check integrity and scaling |
| `notebooks/02_spectra.ipynb` | Welch spectra per axis, comparison across conditions and RPM |
| `notebooks/03_order_and_envelope.ipynb` | RPM-normalised (order) spectra; envelope analysis for bearing defect frequencies computed from bearing geometry |
| `notebooks/04_acoustic.ipynb` | Acoustic spectra and band energies; comparison between microphone and piezo if both are tried |
| `notebooks/05_thermal.ipynb` | Housing vs ambient temperature, rise rates under load |
| `notebooks/06_feature_candidates.ipynb` | Distributions of candidate features per condition; separability and RPM dependence |
| `sa/` (package) | Reusable loading and plotting helpers used by the notebooks |
| `requirements.txt` | Pinned dependencies |

## Rules

- Notebooks are committed **without outputs** (clear outputs before committing) to keep the repository
  small and avoid embedding data; curated figures go to `media/diagrams/` or `models/evaluation/`.
- Every figure must state the `recording_id`(s) it was produced from.
- No conclusions about detection capability may be drawn from a single run.

## Current status

- No notebooks; no data.

## TODO

- [ ] Create the helper package and the first notebook after the first healthy-baseline recordings.
- [ ] Compute bearing characteristic frequencies from catalogue geometry for the selected bearing.
- [ ] Document findings that lead to the feature definition in `firmware/dsp/README.md`.
