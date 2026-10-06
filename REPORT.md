# Largest (X/E) การทดสอบ YOLO Instance Segmentation — MOTS20

## 1. สถานะการทดลอง

PASS WITH WARNINGS

- โมเดลที่เสร็จแล้ว: 4/4
- จำนวนเฟรม: 2,862 ต่อโมเดล; Person GT รายเฟรม: 26,894 instances
- รหัสรอบทดลอง: `benchmark-20260929T0520Z`

## 2. โมเดลที่ทดสอบ

| ตระกูล | โมเดล | จำนวนพารามิเตอร์ | GFLOPs | Checkpoint (MB) |
| --- | --- | --- | --- | --- |
| YOLO26 | YOLO26x-Seg | 70,693,800 | 338.203 | 142.13 |
| YOLO11 | YOLO11x-Seg | 62,142,656 | 297.892 | 125.09 |
| YOLOv9 | YOLOv9e-Seg | 60,512,800 | 238.333 | 122.21 |
| YOLOv8 | YOLOv8x-Seg | 71,827,888 | 329.189 | 144.10 |

## 3. ความสอดคล้องกับโพรโทคอล

| รายการ | สถานะ |
|---|---|
| ข้อมูล | PASS |
| ตัวประเมิน | PASS |
| การเตรียมภาพ | PASS |
| ขนาดภาพเข้าโมเดล | PASS |
| ความละเอียดเชิงตัวเลข | PASS |
| ค่าเกณฑ์ | PASS |
| maxDet | PASS |
| วิธีวัดเวลา | PASS |
| สภาพแวดล้อม | PASS |

ความสอดคล้องของข้อมูล: PASS

ความสอดคล้องของการเตรียมภาพ: PASS

[วิธีทดลองร่วม](https://github.com/folklazy/YOLO_Instance_Segmentation_MOTS20_Scaling_Study/blob/main/METHODOLOGY_REFERENCE.md) · [โพรโทคอลการทดลอง](EXPERIMENT_PROTOCOL.md) · [หลักฐานการกำหนดมาตรฐาน](manifests/STANDARDIZATION.json)

## 4. ผลลัพธ์รวม

| โมเดล | Mask mAP50-95 | AP50 | AP75 | Precision | Recall | F1 | TP-only IoU | TP-only Dice | Inference (ms) | Pipeline (ms) | FPS | Peak allocated VRAM (MiB) | จำนวนพารามิเตอร์ | GFLOPs | Checkpoint (MB) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| YOLO26x-Seg | 0.603730 | 0.903687 | 0.664426 | 0.946008 | 0.846285 | 0.893372 | 0.828873 | 0.902919 | 72.458 | 109.639 | 9.121 | 952.18 | 70,693,800 | 338.203 | 142.13 |
| YOLO11x-Seg | 0.536674 | 0.875806 | 0.575845 | 0.938702 | 0.822228 | 0.876613 | 0.801385 | 0.886046 | 69.406 | 105.885 | 9.444 | 942.48 | 62,142,656 | 297.892 | 125.09 |
| YOLOv9e-Seg | 0.536642 | 0.882037 | 0.572100 | 0.934230 | 0.826578 | 0.877113 | 0.799298 | 0.884605 | 65.888 | 103.376 | 9.673 | 855.41 | 60,512,800 | 238.333 | 122.21 |
| YOLOv8x-Seg | 0.524758 | 0.866402 | 0.560452 | 0.921598 | 0.814271 | 0.864616 | 0.798136 | 0.883841 | 67.843 | 109.441 | 9.137 | 1001.13 | 71,827,888 | 329.189 | 144.10 |

## 5. ผู้ชนะในแต่ละด้าน

| ด้าน | โมเดล | ผลลัพธ์ |
| --- | --- | --- |
| Mask mAP50-95 สูงสุด | YOLO26x-Seg | 0.603730 |
| AP75 สูงสุด | YOLO26x-Seg | 0.664426 |
| Recall สูงสุด | YOLO26x-Seg | 0.846285 |
| Inference เร็วสุด | YOLOv9e-Seg | 65.888 |
| Pipeline เร็วสุด | YOLOv9e-Seg | 103.376 |
| FPS สูงสุด | YOLOv9e-Seg | 9.673 |
| VRAM ต่ำสุด | YOLOv9e-Seg | 855.41 |

## 6. ข้อค้นพบสำคัญ

- ข้อสังเกต: YOLO26x-Seg มี Mask mAP50-95 สูงสุด 0.603730; ห่างอันดับถัดไป 0.067056 บนสเกล 0–1
- ข้อสังเกต: YOLO26x-Seg นำ AP75; YOLO26x-Seg นำ Recall
- ข้อสังเกต: YOLOv9e-Seg มี inference เร็วสุด; YOLOv9e-Seg มี pipeline เร็วสุดและ FPS สูงสุด; YOLOv9e-Seg มี VRAM ต่ำสุด
- คู่ mAP ใกล้ที่สุด: YOLO11x-Seg / YOLOv9e-Seg ต่าง 0.000032; เป็นความใกล้เชิงพรรณนา ไม่ใช่ผลทดสอบนัยสำคัญทางสถิติ
- การตีความ: แยกความแม่นยำความครบถ้วนเวลา forward เวลา pipeline และหน่วยความจำไม่มีคะแนนรวมถ่วงน้ำหนักจำนวนพารามิเตอร์หรือ GFLOPs ไม่กำหนดอันดับเวลา/VRAM โดยตรง

## 7. ข้อสังเกตรายลำดับภาพ

- YOLO26x-Seg: Mask mAP50-95 สูงสุดที่ MOTS20-11 (0.656433); ต่ำสุดที่ MOTS20-02 (0.486317)
- YOLO11x-Seg: Mask mAP50-95 สูงสุดที่ MOTS20-05 (0.604070); ต่ำสุดที่ MOTS20-02 (0.416815)
- YOLOv9e-Seg: Mask mAP50-95 สูงสุดที่ MOTS20-05 (0.602120); ต่ำสุดที่ MOTS20-02 (0.422845)
- YOLOv8x-Seg: Mask mAP50-95 สูงสุดที่ MOTS20-05 (0.586309); ต่ำสุดที่ MOTS20-02 (0.410787)
- ลำดับ mAP ที่ต่างจากผลรวม: MOTS20-02: YOLO26x-Seg > YOLOv9e-Seg > YOLO11x-Seg > YOLOv8x-Seg

AP รวมคำนวณจากข้อมูลทั้งหมด ไม่ใช่ค่าเฉลี่ย AP รายลำดับภาพ ดูค่าครบใน [PER_SEQUENCE_RESULTS.csv](metrics/PER_SEQUENCE_RESULTS.csv)

## 8. ประสิทธิภาพและการใช้ทรัพยากร

- คู่ที่ใกล้ที่สุดด้านค่าเฉลี่ย inference: YOLO11x-Seg / YOLOv8x-Seg ต่าง 1.563 ms; ไม่ได้ทดสอบนัยสำคัญทางสถิติ
- คู่ที่ใกล้ที่สุดด้านค่าเฉลี่ย pipeline: YOLO26x-Seg / YOLOv8x-Seg ต่าง 0.197 ms; ไม่ได้ทดสอบนัยสำคัญทางสถิติ

YOLOv9e-Seg ใช้ peak allocated VRAM ต่ำสุดจำนวนพารามิเตอร์ก่อน/หลัง fusion, GFLOPs และเวลาโหลดแยกเก็บใน [MODEL_COMPLEXITY.csv](metrics/MODEL_COMPLEXITY.csv) ส่วน peak reserved VRAM อยู่ใน [แหล่งวัดเวลา](timing/benchmark-20260929T0520Z/clean_repetition/summary.csv) เวลาเตรียม RLE แยก: yolo26x-seg.pt: 205.007 ms; yolo11x-seg.pt: 195.782 ms; yolov9e-seg.pt: 215.136 ms; yolov8x-seg.pt: 232.719 ms.

ใช้ 3 รอบที่ไม่ถูกรบกวนต่อโมเดล รอบละ 100 เฟรมหลัง 10 warmups และ synchronize CUDA ตามขอบเขต stage ค่า pipeline รวม preprocessing, inference และ postprocessing ไม่รวมการเตรียม RLE และการอ่านเขียนดิสก์ FPS จึงไม่ใช่อัตราการบันทึก mask ครบกระบวนการและไม่บวก Ultralytics-inclusive diagnostic ซ้ำ

ค่าเฉลี่ย postprocessing: YOLO26x-Seg: 35.464 ms; YOLO11x-Seg: 34.797 ms; YOLOv9e-Seg: 35.790 ms; YOLOv8x-Seg: 39.887 ms

## 9. คำเตือนและข้อสังเกตผิดปกติ

เก็บสถานะ PASS WITH WARNINGS จากรอบเดิม: พบคำเตือน CPU NNPACK ระหว่างตรวจความซับซ้อนโมเดลและคำเตือนเลิกใช้ของ pycocotools/NumPy การตรวจ regression เดิมผ่านและไม่เปลี่ยน package เพื่อซ่อนคำเตือน การวัดเวลารอบแรกของ Largest ถูกตัดออกทั้งชุดเพราะเริ่มเมื่อ GPU ไม่ว่าง ผลหลักใช้ 3 clean repetitions เดิมเท่านั้น

Pipeline ไม่รวมการเตรียม RLE และการอ่านเขียนดิสก์จึงไม่ใช่เวลา/อัตราประมวลผลครบกระบวนการสำหรับการบันทึก mask หรือระบบ CCTV การปรับเอกสารครั้งนี้ไม่รัน inference ใหม่และไม่เปลี่ยนค่าที่วัด

## 10. ข้อจำกัด

ผลนี้เป็น Person instance segmentation รายเฟรมบน MOTS20 ไม่ใช่ MOTS tracking; TP-only IoU/Dice พิจารณาเฉพาะคู่ที่ จับคู่ ได้ ภาพวิดีโอต่อเนื่องสัมพันธ์กันและไม่ได้ทดสอบนัยสำคัญทางสถิติค่าใกล้กันควรอ่านว่าใกล้กันเชิงพรรณนารุ่น E/X และ C/L ไม่ใช่ capacity เท่ากัน ผลยังไม่ยืนยันภาพพร่า, แสงน้อย, มุมกล้อง, ระดับ occlusion หรือความพร้อมใช้งาน CCTV; เป็นตัวเลือกสำหรับการทดสอบต่อการประเมินความทนทานต่อ CCTV เท่านั้น

## 11. หลักฐานสำหรับตรวจสอบซ้ำ

- [TIER_RESULTS.csv](metrics/TIER_RESULTS.csv)
- [PER_SEQUENCE_RESULTS.csv](metrics/PER_SEQUENCE_RESULTS.csv)
- [TIMING_SUMMARY.csv](metrics/TIMING_SUMMARY.csv)
- [MODEL_COMPLEXITY.csv](metrics/MODEL_COMPLEXITY.csv)
- [PREFLIGHT_MAXDET.csv](metrics/PREFLIGHT_MAXDET.csv)

[แหล่งที่มาและค่า hash](manifests/STANDARDIZATION.json) · [โพรโทคอล](EXPERIMENT_PROTOCOL.md) · [รายการกราฟ](outputs/plots/INDEX.md) · [บันทึกย้อนหลัง](reports/archive/)

prediction แบบ RLE ที่ไม่สูญเสียข้อมูลและบันทึกการวัดเวลาละเอียดเก็บในเครื่องตามรหัสรอบทดลอง หลักฐานต้นทางคงเดิม; การปรับภาษานี้ไม่คำนวณค่าตัวชี้วัดใหม่และไม่รัน inference

## 12. ความเชื่อมโยงกับการศึกษาทุกขนาด

[การศึกษาหลัก](https://github.com/folklazy/YOLO_Instance_Segmentation_MOTS20_Scaling_Study) — รายงานนี้กล่าวถึงขนาด Largest (X/E) เท่านั้นผลรวม 17 โมเดลยังรอคำสั่งจากผู้ใช้ แม้การทดลองทั้งห้าขนาดเสร็จแล้ว การปรับเอกสารไม่เริ่ม benchmark หรือการสังเคราะห์ผลใหม่

## การวิเคราะห์เชิงคุณภาพ

ภาพเปรียบเทียบเฟรมเดียวกัน 4 กรณีจาก prediction ที่บันทึกไว้ พร้อมข้อผิดพลาดที่พบและการตีความ อยู่ใน [PRESENTATION_SUMMARY_TH.md](PRESENTATION_SUMMARY_TH.md) ดู [เหตุผลเลือกกรณีปัจจุบัน](outputs/visualizations/qualitative/selection_v2/CASE_SELECTION.md) และ [ตัวชี้ชุดหลักฐาน](manifests/QUALITATIVE_SELECTION.json) รายงานเทคนิคนี้เชื่อมไปยังการวิเคราะห์ภาพเพื่อไม่เล่าเนื้อหาซ้ำ
