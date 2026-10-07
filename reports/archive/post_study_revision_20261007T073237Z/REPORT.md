# Largest (X/E) YOLO Segmentation Benchmark — MOTS20

## 1. Experiment Status

PASS WITH WARNINGS

- Models completed: 4/4
- Frames: 2,862 per model; Person GT instances: 26,894
- Run ID: `benchmark-20260929T0520Z`

## 2. Models Tested

| Family | Model | Parameters | GFLOPs | Checkpoint MB |
| --- | --- | --- | --- | --- |
| YOLO26 | YOLO26x-Seg | 70,693,800 | 338.203 | 142.13 |
| YOLO11 | YOLO11x-Seg | 62,142,656 | 297.892 | 125.09 |
| YOLOv9 | YOLOv9e-Seg | 60,512,800 | 238.333 | 122.21 |
| YOLOv8 | YOLOv8x-Seg | 71,827,888 | 329.189 | 144.10 |


## 3. Protocol Compatibility

| Item | Status |
|---|---|
| Dataset | PASS |
| Evaluator | PASS |
| Preprocessing | PASS |
| Input size | PASS |
| Precision | PASS |
| Thresholds | PASS |
| maxDet | PASS |
| Timing protocol | PASS |
| Environment | PASS |

Dataset compatibility: PASS

Preprocessing compatibility: PASS

Historical environment and frozen evidence verified; shared methodology: [Master Study](https://github.com/folklazy/YOLO_Instance_Segmentation_MOTS20_Scaling_Study).

## 4. Overall Results

| Model | Mask mAP50-95 | AP50 | AP75 | Precision | Recall | F1 | TP-only IoU | TP-only Dice | Inference ms | Pipeline ms | FPS | Peak VRAM MiB | Params | GFLOPs | Checkpoint MB |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| YOLO26x-Seg | 0.603730 | 0.903687 | 0.664426 | 0.946008 | 0.846285 | 0.893372 | 0.828873 | 0.902919 | 72.458 | 109.639 | 9.121 | 952.18 | 70,693,800 | 338.203 | 142.13 |
| YOLO11x-Seg | 0.536674 | 0.875806 | 0.575845 | 0.938702 | 0.822228 | 0.876613 | 0.801385 | 0.886046 | 69.406 | 105.885 | 9.444 | 942.48 | 62,142,656 | 297.892 | 125.09 |
| YOLOv9e-Seg | 0.536642 | 0.882037 | 0.572100 | 0.934230 | 0.826578 | 0.877113 | 0.799298 | 0.884605 | 65.888 | 103.376 | 9.673 | 855.41 | 60,512,800 | 238.333 | 122.21 |
| YOLOv8x-Seg | 0.524758 | 0.866402 | 0.560452 | 0.921598 | 0.814271 | 0.864616 | 0.798136 | 0.883841 | 67.843 | 109.441 | 9.137 | 1001.13 | 71,827,888 | 329.189 | 144.10 |


## 5. Tier Winners

| Category | Model | Value |
|---|---|---|
| Highest Mask mAP50-95 | YOLO26x-Seg | 0.603730 |
| Highest AP75 | YOLO26x-Seg | 0.664426 |
| Highest Recall | YOLO26x-Seg | 0.846285 |
| Fastest inference | YOLOv9e-Seg | 65.888 |
| Fastest pipeline | YOLOv9e-Seg | 103.376 |
| Highest FPS | YOLOv9e-Seg | 9.673 |
| Lowest VRAM | YOLOv9e-Seg | 855.41 |

Inference and pipeline latency are in ms/frame; FPS is derived from mean pipeline latency; VRAM is peak allocated MiB.

## 6. Key Findings

- Observed highest Mask mAP50-95: YOLO26x-Seg (0.603730).
- Lowest inference mean: YOLOv9e-Seg; lowest pipeline mean: YOLOv9e-Seg. These are distinct measurements.
- Lowest allocated VRAM: YOLOv9e-Seg (855.41 MiB).
- Interpretation: choose by measured accuracy, latency and memory constraints; no weighted score or architecture-causality claim.
- YOLO11x-Seg and YOLOv9e-Seg have descriptively near-tied Mask mAP50-95; the tiny difference is not evidence of statistical superiority.

## 7. Per-sequence Observations

- YOLO26x-Seg: strongest MOTS20-11 (0.656433); weakest MOTS20-02 (0.486317) by sequence Mask mAP50-95.
- YOLO11x-Seg: strongest MOTS20-05 (0.604070); weakest MOTS20-02 (0.416815) by sequence Mask mAP50-95.
- YOLOv9e-Seg: strongest MOTS20-05 (0.602120); weakest MOTS20-02 (0.422845) by sequence Mask mAP50-95.
- YOLOv8x-Seg: strongest MOTS20-05 (0.586309); weakest MOTS20-02 (0.410787) by sequence Mask mAP50-95.

## 8. Efficiency and Resource Observations

YOLOv9e-Seg has the lowest measured inference mean; YOLOv9e-Seg has the lowest pipeline mean and highest mean-derived FPS. YOLOv9e-Seg has the lowest allocator peak. Loaded parameters and NMS-path GFLOPs are in the table; fused runtime counts and separate loading times are in MODEL_COMPLEXITY.csv. Parameter counts do not imply proportional VRAM or latency.

## 9. Warnings and Anomalies

Historical PASS WITH WARNINGS retained: CPU NNPACK warnings during complexity inspection and pycocotools/NumPy deprecation warnings. Historical regression checks passed; no dependency changes were made. Pipeline excludes RLE preparation and disk I/O, so FPS is not end-to-end saved-mask throughput. The original Largest timing pass was excluded in its entirety for non-idle starts; all primary measurements use three clean historical repetitions.

## 10. Limitations

This evaluates frame-level Person instance segmentation on MOTS20, rather than MOTS tracking. The 26,894 GT instances are frame-level annotations, not unique people. TP-only IoU/Dice are conditional on successful matching.

Consecutive video frames are correlated, and no statistical significance test was performed; small differences are descriptive. Selected qualitative cases do not replace dataset-level metrics.

The E/X and C/L checkpoints do not have equal capacity. These measurements do not establish robustness to blur, low light, camera angle or occlusion severity, or deployment suitability. They support candidate selection for later CCTV robustness evaluation only. No weighted score or architectural causal conclusion is used.

## 11. Reproducibility and Source Artifacts

- [TIER_RESULTS.csv](metrics/TIER_RESULTS.csv)
- [PER_SEQUENCE_RESULTS.csv](metrics/PER_SEQUENCE_RESULTS.csv)
- [TIMING_SUMMARY.csv](metrics/TIMING_SUMMARY.csv)
- [MODEL_COMPLEXITY.csv](metrics/MODEL_COMPLEXITY.csv)
- [PREFLIGHT_MAXDET.csv](metrics/PREFLIGHT_MAXDET.csv)

[Standardization provenance](manifests/STANDARDIZATION.json) · [Frozen protocol](EXPERIMENT_PROTOCOL.md) · [Historical reports](reports/archive/)

[Canonical plots](outputs/plots/INDEX.md).

## 12. Relation to Full Scaling Study

[Master Study](https://github.com/folklazy/YOLO_Instance_Segmentation_MOTS20_Scaling_Study) — this is one tier only. The 17-model synthesis remains gated on all five tiers and explicit authorization.

## Qualitative Analysis

Four same-frame diagnostic comparisons from saved lossless predictions are discussed in [PRESENTATION_SUMMARY_TH.md](PRESENTATION_SUMMARY_TH.md). See [current case selection](outputs/visualizations/qualitative/selection_v2/CASE_SELECTION.md) and [active selection](manifests/QUALITATIVE_SELECTION.json) for selection reasons, shared and tier-specific behaviors, and evidence limits. Comparisons use original MOTS20 frames. No inference or measured values were changed for this documentation update.
