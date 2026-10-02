# Largest available YOLO segmentation variants: MOTS20

[📊 อ่านสรุปผล Benchmark แบบเข้าใจง่าย (ภาษาไทย)](BENCHMARK_INSIGHTS_TH.md)

Read [REPORT.md](REPORT.md) for human-readable results and execution status,
and [EXPERIMENT_PROTOCOL.md](EXPERIMENT_PROTOCOL.md) for the frozen methodology.
The validated `Person_Segmentation_Pilot` is unchanged; evaluator snapshots and
their original SHA256 hashes are under `src/frozen_pilot/` and `manifests/`.

Completed run `benchmark-20260929T0520Z`: **PASS WITH WARNINGS**. All four models
processed 2,862 frames; 36 final consistency checks passed. Common AP maxDet=200.
YOLO26x had highest mask accuracy; YOLOv9e had fastest inference and lowest peak
allocated VRAM. The initial timing pass was excluded for non-idle start flags;
all four models completed a new clean pass with three rounds each. Primary speed
data are in `timing/benchmark-20260929T0520Z/clean_repetition/`. The original pass
is preserved. See the report for exact values, qualifications and provenance.

Use workspace `.venv/bin/python` directly. No packages were changed. Dependencies
and runtime build versions are frozen in `manifests/environment.json`.
All model checkpoints are shared in workspace `models/`; all inputs stay under
workspace `datasets/MOTS/MOTS/train/`. No split or dataset conversion is created.

The runner resolves workspace paths from its own location. Run from the workspace:

```bash
.venv/bin/python -u -B YOLO_Large_Seg_MOTS20_Benchmark/src/validate.py
.venv/bin/python -u -B YOLO_Large_Seg_MOTS20_Benchmark/src/benchmark.py preflight RUN_ID
.venv/bin/python -u -B YOLO_Large_Seg_MOTS20_Benchmark/src/benchmark.py full RUN_ID
.venv/bin/python -u -B YOLO_Large_Seg_MOTS20_Benchmark/src/benchmark.py timing RUN_ID
.venv/bin/python -u -B YOLO_Large_Seg_MOTS20_Benchmark/src/report.py RUN_ID
```

For this run, after the initial timing pass finished, the documented idle-gated
replacement used `src/repeat_clean_timing.py RUN_ID`; reporting used
`src/report_clean_timing.py RUN_ID`, then `src/refine_scatter_plots.py RUN_ID` to
replace overlapping scatter labels with legends. These retain original source
and artifacts. Exact generated timing/report source and substitutions are
archived in `logs/RUN_ID/`. Measurement definitions and accuracy were unchanged.

These are reproduction instructions, not permission to overwrite a prior run.
Inference directories must be fresh. A new experiment repetition must preserve
previous manifests/config/protocol, reset the preflight selection in a new
versioned protocol, and retain old reports. Stop on a failed phase, OOM, cap
saturation or dependency incompatibility. Do not run full/timing after failed
preflight. Saved predictions are per-frame atomic gzip JSON with lossless native
COCO RLE and enough metadata for metric regeneration without inference.

No equal-capacity, tracking, or CCTV-robustness conclusion is supported by design.
