# Model Evaluation (`models/evaluation`)

**Status: Placeholder** - no evaluation has been performed; no results exist.

## Purpose

This directory defines how BearingGuard AI models will be evaluated and stores the resulting
summaries (tables and plots). It exists so that every claim about detection performance can be traced
to a documented protocol and a reproducible result.

## Expected files

| File | Planned content |
|---|---|
| `evaluation_protocol.md` | Dataset partitions by run, metrics, threshold-selection method, per-condition and per-RPM breakdowns, statistical reporting (confidence intervals where possible) |
| `metrics.md` | Definitions: anomaly-score distributions for healthy vs. each fault condition, ROC / precision-recall for "deviation present", false-positive rate on held-out healthy runs, detection delay (time from fault onset in a run to Orange/Red), stability of the health score over long healthy runs |
| `results/` | Generated tables and plots per experiment - **ignored by git**; curated summary plots may be copied to `media/diagrams/` or embedded in a results Markdown file |
| `results_summary.md` | Human-readable summary of the latest evaluation with the experiment ID it refers to |

## Planned evaluation principles

- **Run-level splits only.** Windows from the same run never appear in more than one partition.
- **Healthy false alarms matter most.** A device that cries wolf will be ignored; held-out healthy runs
  at all speeds and loads are the primary stress test.
- **Report per condition and per severity.** A single aggregate number hides where the model fails.
- **Report detection delay**, not only whether a condition is eventually flagged.
- **Separate validation from test.** Thresholds are chosen on validation runs and reported on test runs.
- **No cherry-picking.** Every experiment logged in `../training/experiments.md` has its evaluation recorded.

## Current status

- Protocol not yet written; no data.

## TODO

- [ ] Write `evaluation_protocol.md` and `metrics.md` before the first training experiment.
- [ ] Decide acceptance criteria for the first on-device deployment.
- [ ] Add scripts for generating the result tables to `tools/model_training/`.
