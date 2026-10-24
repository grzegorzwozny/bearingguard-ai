# Example Data (`datasets/examples`)

**Status: Placeholder** - no example files exist yet.

## Purpose

This directory will hold a very small number of **small, clearly documented example files** used to
test and demonstrate the tooling (capture-file readers, feature extraction, metadata validation)
without requiring access to the external data store. Examples are for software testing, not for
drawing conclusions about bearing behaviour.

## What may be placed here

| Allowed | Not allowed |
|---|---|
| A short synthetic signal (for example a few seconds of generated sine plus noise) with a generation script | Any file presented as a real measurement that was not actually recorded |
| A truncated excerpt of a real run **once recordings exist**, if it is small (well under 1 MB), fully described, and contains no raw audio with speech | Raw audio, long recordings, or anything that would bloat the repository |
| A metadata CSV with rows that are explicitly labelled as examples and reference example files only | Fabricated metadata rows presented as real runs |

Every example must be accompanied by a `README` entry stating: origin (`synthetic` or `measured`),
how it was generated or excerpted, sample rate, units, and the `recording_id` if derived from a real run.

## Expected files (planned)

| File | Planned content |
|---|---|
| `synthetic_example_accel.npy` | Generated three-axis signal for reader and feature tests |
| `synthetic_example_meta.json` | Metadata for the synthetic example, `data_origin: synthetic` |
| `make_synthetic_example.py` | Script that regenerates the synthetic example deterministically |
| `examples_index.md` | Table of all example files with origin and purpose |

## Current status

- Empty; the tooling that would consume examples does not exist yet.

## TODO

- [ ] Add the synthetic example generator together with the first reader implementation in `tools/`.
- [ ] Add `examples_index.md` and keep it updated.
