# สรุปผล Largest (X/E) YOLO Instance Segmentation

## สรุปใน 1 นาที

- โมเดล: YOLO26x-Seg, YOLO11x-Seg, YOLOv9e-Seg, YOLOv8x-Seg
- MOTS20 2,862 frames / 26,894 Person GT instances (annotation รายเฟรม)
- Official pretrained checkpoints / no fine-tuning; สถานะเดิม PASS WITH WARNINGS
- Accuracy สูงสุด: YOLO26x-Seg — Mask mAP50-95 0.603730
- เร็วสุด: inference YOLOv9e-Seg (65.888 ms); pipeline YOLOv9e-Seg (103.376 ms)
- Peak allocated VRAM ต่ำสุด: YOLOv9e-Seg — 855.41 MiB
- Trade-off หลัก: YOLO26x-Seg นำรองอันดับสอง 6.705603 percentage points ของ mAP; เวลา inference มากกว่าตัวเร็วสุด 6.570 ms

## ผลลัพธ์หลัก

| Model | Mask mAP50-95 | AP75 | Recall | Inference ms | Pipeline ms | FPS | Peak VRAM MiB |
|---|---|---|---|---|---|---|---|
| YOLO26x-Seg | 0.603730 | 0.664426 | 0.846285 | 72.458 | 109.639 | 9.121 | 952.18 |
| YOLO11x-Seg | 0.536674 | 0.575845 | 0.822228 | 69.406 | 105.885 | 9.444 | 942.48 |
| YOLOv9e-Seg | 0.536642 | 0.572100 | 0.826578 | 65.888 | 103.376 | 9.673 | 855.41 |
| YOLOv8x-Seg | 0.524758 | 0.560452 | 0.814271 | 67.843 | 109.441 | 9.137 | 1001.13 |

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

- mAP ของ YOLO26x-Seg สูงกว่า YOLO11x-Seg 6.705603 percentage points
- YOLO11x และ YOLOv9e มี mAP ต่างกันเพียง 0.000032 (0.003190 percentage points); เป็น descriptive near tie
- YOLOv8x มี peak VRAM สูงสุด 1001.13 MiB แต่ mAP ต่ำสุดใน tier
- Accuracy winner ใช้ VRAM มากกว่าตัวต่ำสุด 96.78 MiB; การจัดอันดับ inference และ pipeline ต้องแยกกัน

## Trade-off หลัก

### Accuracy vs Speed

YOLO26x-Seg มี mAP 0.603730; YOLOv9e-Seg มี mAP 0.536642
และ inference 65.888 ms เทียบกับ 72.458 ms ของ accuracy winner
Pipeline winner คือ YOLOv9e-Seg (103.376 ms); ไม่ใช้เวลา forward แทน throughput ของ pipeline

### Accuracy vs Memory

YOLO26x-Seg ใช้ 952.18 MiB; YOLOv9e-Seg ใช้ 855.41 MiB
และมี mAP 0.536642

## ข้อควรระวังในการตีความ

ไม่มีการทดสอบ statistical significance; near tie เป็นคำบรรยาย ค่า AP/Recall อยู่ช่วง 0–1
Pipeline ไม่รวม RLE preparation และ disk I/O; VRAM เป็น peak allocated
MOTS20 ไม่ใช่ผลทดสอบ CCTV robustness ขั้นสุดท้าย และ E/X, C/L ไม่ใช่ capacity เท่ากัน

## ข้อมูลสำหรับนำไปรวมต่อ

นำ YOLO26x สำหรับ accuracy และ YOLOv9e สำหรับ speed/VRAM; เก็บ YOLO11x เป็นคู่ near tie ของ YOLOv9e ไปเทียบข้าม tier โดยคง protocol และแหล่ง canonical เดิม ยังไม่สรุปครบ 17 โมเดล

[TIER_RESULTS.csv](metrics/TIER_RESULTS.csv) · [REPORT.md](REPORT.md) ·
[Visual analysis](PRESENTATION_SUMMARY_TH.md) ·
[Master Study](https://github.com/folklazy/YOLO_Instance_Segmentation_MOTS20_Scaling_Study)
