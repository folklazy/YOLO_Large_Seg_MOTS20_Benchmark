# Qualitative case selection

Pool: the 12 frozen frames in manifests/visualization_frames.json, reviewed using existing
per-frame CSVs and actual comparisons. Diagnostic selection, not random or representative sampling.
The set includes an advantage, shared failure, counterexample and similar-output check.
No inference; source frame / GT / prediction / comparison SHA256 and per-frame counts are in CASE_EVIDENCE.json.
Counts were checked against existing CSVs. All panels show the same full frame at the same scale.

| Case | Sequence | Frame | Reason | Model behavior |
|---|---|---|---|---|
| 1 | MOTS20-05 | 000419 | additional valid small Person; retain shared FN | YOLO26x-Seg: TP/FP/FN 5/0/1; YOLO11x-Seg: TP/FP/FN 5/0/1; YOLOv9e-Seg: TP/FP/FN 5/0/1; YOLOv8x-Seg: TP/FP/FN 4/0/2 |
| 2 | MOTS20-09 | 000263 | shared misses / unmatched masks | YOLO26x-Seg: TP/FP/FN 9/2/4; YOLO11x-Seg: TP/FP/FN 9/2/4; YOLOv9e-Seg: TP/FP/FN 8/1/5; YOLOv8x-Seg: TP/FP/FN 8/1/5 |
| 3 | MOTS20-02 | 000600 | counterexample to aggregate ranking / detection trade-off | YOLO26x-Seg: TP/FP/FN 9/0/1; YOLO11x-Seg: TP/FP/FN 10/0/0; YOLOv9e-Seg: TP/FP/FN 9/0/1; YOLOv8x-Seg: TP/FP/FN 10/1/0 |
| 4 | MOTS20-09 | 000001 | similar valid detections / near-tie context | YOLO26x-Seg: TP/FP/FN 6/0/0; YOLO11x-Seg: TP/FP/FN 6/0/0; YOLOv9e-Seg: TP/FP/FN 6/0/0; YOLOv8x-Seg: TP/FP/FN 6/0/0 |

Only observed failure types are discussed. No inferred error frequency, scene severity or statistical significance.
