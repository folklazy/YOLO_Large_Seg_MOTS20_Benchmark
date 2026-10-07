# สรุปผล Largest (X/E) YOLO Instance Segmentation

## สรุปใน 1 นาที

- โมเดล: YOLO26x-Seg, YOLO11x-Seg, YOLOv9e-Seg, YOLOv8x-Seg
- MOTS20 2,862 frames / 26,894 Person GT instances รายเฟรม
- Official pretrained checkpoints; ไม่มี training หรือ fine-tuning; สถานะ PASS WITH WARNINGS
- Accuracy สูงสุด: YOLO26x-Seg — Mask mAP50-95 0.603730
- Inference เร็วสุด: YOLOv9e-Seg — 65.888 ms
- Pipeline เร็วสุด: YOLOv9e-Seg — 103.376 ms / 9.673 FPS
- Peak allocated VRAM ต่ำสุด: YOLOv9e-Seg — 855.41 MiB
- Trade-off หลัก: ตัวนำ mAP สูงกว่ารองอันดับสอง 6.706 percentage points; ต้องแยก forward จาก pipeline

## ผลลัพธ์หลัก

| Model | Mask mAP50-95 | AP75 | Recall | Inference ms | Pipeline ms | FPS | Peak VRAM MiB |
|---|---|---|---|---|---|---|---|
| YOLO26x-Seg | 0.603730 | 0.664426 | 0.846285 | 72.458 | 109.639 | 9.121 | 952.18 |
| YOLO11x-Seg | 0.536674 | 0.575845 | 0.822228 | 69.406 | 105.885 | 9.444 | 942.48 |
| YOLOv9e-Seg | 0.536642 | 0.572100 | 0.826578 | 65.888 | 103.376 | 9.673 | 855.41 |
| YOLOv8x-Seg | 0.524758 | 0.560452 | 0.814271 | 67.843 | 109.441 | 9.137 | 1001.13 |

AP/Recall เป็น fraction ช่วง 0–1; latency เป็น ms/frame และ FPS มาจาก mean pipeline

## Winner ของแต่ละด้าน

| ด้าน | Model | Result |
|---|---|---|
| Mask mAP50-95 | YOLO26x-Seg | 0.603730 |
| AP75 | YOLO26x-Seg | 0.664426 |
| Recall | YOLO26x-Seg | 0.846285 |
| Inference speed | YOLOv9e-Seg | 65.888 ms |
| Pipeline speed | YOLOv9e-Seg | 103.376 ms |
| VRAM | YOLOv9e-Seg | 855.41 MiB |

## สิ่งที่ตัวเลขบอกเรา

- YOLO26x-Seg นำ YOLO11x-Seg ด้าน mAP 6.706 percentage points
- YOLO11x/YOLOv9e เป็น descriptive near tie ของ mAP; AP75 นำใน YOLO11x แต่ Recall และทรัพยากรนำใน YOLOv9e
- YOLOv8x forward เร็วกว่า YOLO26x แต่ pipeline ใกล้กัน และใช้ VRAM มากกว่า
- YOLO11x-Seg/YOLOv9e-Seg: ต่าง 0.003190 percentage points; near tie ไม่ใช่ equivalence หรือ statistical significance

## บทบาทของแต่ละโมเดล

| Model | จุดเด่น | สิ่งที่แลก | เหมาะพิจารณาเมื่อ |
|---|---|---|---|
| YOLO26x-Seg | นำ mAP/AP75/Recall และ TP-only quality | Inference ช้าที่สุด; VRAM สูงกว่า YOLOv9e | ยอมเพิ่ม latency เพื่อ accuracy |
| YOLO11x-Seg | mAP near-tied กับ YOLOv9e; AP75 สูงกว่าเล็กน้อย | Recall ต่ำกว่าและ latency/VRAM สูงกว่า YOLOv9e | ตรวจ trade-off ของ mask overlap กับ coverage |
| YOLOv9e-Seg | Inference/pipeline เร็วสุด; VRAM ต่ำสุด | mAP/AP75 ต่ำกว่า YOLO26x | Latency หรือ memory เป็นข้อจำกัด |
| YOLOv8x-Seg | Forward เร็วกว่า YOLO11x/YOLO26x | mAP ต่ำสุด; VRAM สูงสุด; pipeline ใกล้ YOLO26x | ต้องการ baseline รุ่นก่อน |

## Trade-off หลัก

### Accuracy vs Speed

YOLO26x-Seg มี mAP 0.603730; ตัว forward เร็วสุด YOLOv9e-Seg มี mAP 0.536642 และ inference ต่ำกว่า 6.570 ms ส่วน pipeline ต้องดู YOLOv9e-Seg แยก ไม่ถือว่า forward winner เป็น throughput winner

### Accuracy vs Memory

YOLO26x-Seg ใช้ VRAM มากกว่า YOLOv9e-Seg 96.78 MiB เพื่อ mAP สูงกว่า 6.709 percentage points ไม่ใช้ชื่อขนาดหรือ parameters แทน memory measurement

## ข้อควรระวังในการตีความ

ไม่มี significance test; ภาพวิดีโอสัมพันธ์กัน TP-only quality วัดเฉพาะคู่ที่ match และ Recall เป็น mask matching ไม่ใช่ box Recall Pipeline ไม่รวม decode, RLE preparation และการเขียนผล; VRAM เป็น peak allocated ภายใต้ benchmark นี้ การแบ่ง tier ไม่ทำให้ capacity/pretraining เท่ากัน และยังไม่ยืนยัน CCTV robustness ไม่มี weighted score หรือผู้ชนะทุกข้อจำกัด

## รายละเอียดเพิ่มเติม

[REPORT.md](REPORT.md) · [รายงานวิจัยภาพเชิงคุณภาพ](PRESENTATION_SUMMARY_TH.md) · [TIER_RESULTS.csv](metrics/TIER_RESULTS.csv) · [Master Study](https://github.com/folklazy/YOLO_Instance_Segmentation_MOTS20_Scaling_Study)
