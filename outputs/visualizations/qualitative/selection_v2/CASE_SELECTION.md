# Large — qualitative case selection v2

Selected from 12 frozen visualization frames using per-frame metrics, original/GT images and saved RLE masks at confidence ≥0.25 and mask matching IoU ≥0.50, with the original evaluator and ignore policy. No inference was run.

One shared anchor plus three cases selected for tier-specific behavior. Tiers need not share every frame; within each case, all models use the same full frame. ROI views supplement the full comparison and do not hide errors elsewhere.

| Case | Sequence / frame | Why selected / decision use | Source comparison |
|---|---|---|---|
| 1 | MOTS20-09 / 000525 | Tier diagnostic: additional GT and fewer unmatched outputs. Compare coverage with extra masks: YOLO26x recovers GT 2003 with no FP, whereas YOLOv9e recovers GT 2004 missed by YOLO26x; both have TP 7. | new composite from saved predictions |
| 2 | MOTS20-09 / 000263 | Shared anchor: common failure. Check coverage of people positioned between other people and instance separation before choosing a model; every model still has errors. | reuse existing image |
| 3 | MOTS20-02 / 000600 | Counterexample and near-tied pair. YOLO11x matches GT 2029, whereas YOLOv9e does not. YOLOv8x recovers all valid GT but produces an extra mask at the right edge. | reuse existing image |
| 4 | MOTS20-11 / 000450 | Near-tied pair: the same valid GT with different extra outputs. YOLO11x and YOLOv9e recover all valid GT, but YOLOv9e has two FP masks while YOLO11x has none in this frame. | new composite from saved predictions |

## Why some frames are shared across tiers

Case 2 (09/263) compares FN/FP against the same GT. Other frames may repeat when the same error region helps compare different models: 05/419 examines GT 2002 in Second-largest/Medium; 02/1 examines equal counts and different GT sets in Second-largest/Medium; 02/600 provides a counterexample in Largest/Small; 02/300 examines TP–FP trade-offs in Small/Nano; 11/1 examines GT 2016 in Second-largest and GT 2028 with extra masks in Nano; 11/450 compares equal coverage with extra outputs in Largest/Medium. Reused frames are not additional independent evidence.

## Replacement of previous cases

Previous Case 1 (05/419) differentiated YOLOv8x but did not separate YOLO26x/YOLO11x/YOLOv9e as clearly as the replacement. Previous Case 4 (09/1) had TP 6 / FP 0 / FN 0 for every model; its replacement keeps coverage controlled while showing different extra outputs. Previous images and evidence remain unchanged for audit; the previous presentation is retained under reports/archive.

## Scope

Across five tiers, 20 case slots use 10 distinct original frames (previously 6). The selection includes MOTS20-11, common failures and counterexamples, rather than only frames where the accuracy leader wins. The 12-frame pool does not represent the dataset, and these are not claimed to be the most divergent frames among all 2,862. Images do not measure latency, VRAM or statistical significance.

[Candidate pool](CANDIDATE_POOL.json) · [Case evidence](CASE_EVIDENCE.json) · [Focus evidence](FOCUS_EVIDENCE.json) · [Decision audit](CASE_DECISION_AUDIT.json) · [Active selection](../../../../manifests/QUALITATIVE_SELECTION.json)
