# Largest (X/E) YOLO Instance Segmentation Benchmark on MOTS20

## Overview

Pretrained YOLO Person instance segmentation on MOTS20. No training or fine-tuning; frame-level evaluation, not tracking. This tier is part of the controlled 17-checkpoint scaling study.

## Models

| Family | Model | Tier |
|---|---|---|
| YOLO26 | YOLO26x-Seg | Largest (X/E) |
| YOLO11 | YOLO11x-Seg | Largest (X/E) |
| YOLOv9 | YOLOv9e-Seg | Largest (X/E) |
| YOLOv8 | YOLOv8x-Seg | Largest (X/E) |

## Experimental Status

PASS WITH WARNINGS — complete, run `benchmark-20260929T0520Z`; historical inference was not rerun during Stage 0.

## Main Result

| Model | Mask mAP50-95 | Recall | F1 | Inference ms | Pipeline ms | FPS | Peak VRAM MiB |
| --- | --- | --- | --- | --- | --- | --- | --- |
| YOLO26x-Seg | 0.603730 | 0.846285 | 0.893372 | 72.458 | 109.639 | 9.121 | 952.18 |
| YOLO11x-Seg | 0.536674 | 0.822228 | 0.876613 | 69.406 | 105.885 | 9.444 | 942.48 |
| YOLOv9e-Seg | 0.536642 | 0.826578 | 0.877113 | 65.888 | 103.376 | 9.673 | 855.41 |
| YOLOv8x-Seg | 0.524758 | 0.814271 | 0.864616 | 67.843 | 109.441 | 9.137 | 1001.13 |

## Reports

- [PRESENTATION_SUMMARY_TH.md](PRESENTATION_SUMMARY_TH.md)
- [RESULTS_SUMMARY_TH.md](RESULTS_SUMMARY_TH.md)
- [REPORT.md](REPORT.md)
- [EXPERIMENT_PROTOCOL.md](EXPERIMENT_PROTOCOL.md)

## Study Navigation

[Largest](https://github.com/folklazy/YOLO_Large_Seg_MOTS20_Benchmark) | [Second-largest](https://github.com/folklazy/YOLO_Second_Largest_Seg_MOTS20_Benchmark) | [Medium](https://github.com/folklazy/YOLO_Medium_Seg_MOTS20_Benchmark) | [Small](https://github.com/folklazy/YOLO_Small_Seg_MOTS20_Benchmark) | [Nano](https://github.com/folklazy/YOLO_Nano_Seg_MOTS20_Benchmark) | [Master Study](https://github.com/folklazy/YOLO_Instance_Segmentation_MOTS20_Scaling_Study)

## Reproducibility

[configs/](configs/) · [metrics/](metrics/) · [manifests/](manifests/)
