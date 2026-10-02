# สรุปผล Largest (X/E) YOLO Instance Segmentation

## สรุปใน 1 นาที

- ทดสอบ YOLO26x-Seg, YOLO11x-Seg, YOLOv9e-Seg, YOLOv8x-Seg สำหรับ Person instance segmentation
- MOTS20 2,862 frames และ 26,894 Person GT instances เป็น annotation รายเฟรม ไม่ใช่จำนวนบุคคลไม่ซ้ำ
- ใช้ pretrained checkpoints / no fine-tuning ภายใต้ controlled benchmark เดียวกัน
- Accuracy สูงสุด: YOLO26x-Seg — Mask mAP50-95 0.603730
- Inference เร็วสุด: YOLOv9e-Seg; pipeline เร็วสุด: YOLOv9e-Seg
- Peak allocated VRAM ต่ำสุด: YOLOv9e-Seg
- ค่าความต่างเล็กมากเป็นเพียง near-tied descriptively ไม่ได้พิสูจน์ statistical significance
- คง PASS WITH WARNINGS และใช้ผลย้อนหลังเดิมทั้งหมด ไม่รัน inference ใหม่

## ผลหลัก

| Model | Mask mAP50-95 | Recall | F1 | Inference ms | Pipeline ms | FPS | Peak VRAM MiB |
| --- | --- | --- | --- | --- | --- | --- | --- |
| YOLO26x-Seg | 0.603730 | 0.846285 | 0.893372 | 72.458 | 109.639 | 9.121 | 952.18 |
| YOLO11x-Seg | 0.536674 | 0.822228 | 0.876613 | 69.406 | 105.885 | 9.444 | 942.48 |
| YOLOv9e-Seg | 0.536642 | 0.826578 | 0.877113 | 65.888 | 103.376 | 9.673 | 855.41 |
| YOLOv8x-Seg | 0.524758 | 0.814271 | 0.864616 | 67.843 | 109.441 | 9.137 | 1001.13 |


## แต่ละโมเดลเด่นด้านไหน

**YOLO26x-Seg**: อันดับเชิงตัวเลข: accuracy 1, inference speed 4, VRAM ต่ำ 3 จากโมเดลใน tier นี้ จุดเด่นคือ accuracy; จุดที่ด้อยกว่าคือ inference speed / VRAM เหมาะเป็นตัวเลือกเริ่มต้นเมื่อให้ความสำคัญกับ accuracy แต่ต้องตรวจ latency ตามข้อจำกัดจริง

**YOLO11x-Seg**: อันดับเชิงตัวเลข: accuracy 2, inference speed 3, VRAM ต่ำ 2 จากโมเดลใน tier นี้ จุดเด่นคือ accuracy / VRAM; จุดที่ด้อยกว่าคือ inference speed ควรเปรียบเทียบกับตัวนำตามข้อจำกัดของงาน ไม่สรุปว่าลำดับที่ใกล้กันมีนัยสำคัญ

**YOLOv9e-Seg**: อันดับเชิงตัวเลข: accuracy 3, inference speed 1, VRAM ต่ำ 1 จากโมเดลใน tier นี้ จุดเด่นคือ inference speed / VRAM; จุดที่ด้อยกว่าคือ accuracy เหมาะพิจารณาเมื่อจำกัดเวลา forward และยอมรับ accuracy ที่ต่ำกว่าตัวนำได้

**YOLOv8x-Seg**: อันดับเชิงตัวเลข: accuracy 4, inference speed 2, VRAM ต่ำ 4 จากโมเดลใน tier นี้ จุดเด่นคือ inference speed; จุดที่ด้อยกว่าคือ accuracy / VRAM ควรเปรียบเทียบกับตัวนำตามข้อจำกัดของงาน ไม่สรุปว่าลำดับที่ใกล้กันมีนัยสำคัญ

## สิ่งที่น่าสนใจจากรอบนี้

- Observation: YOLO26x-Seg นำด้าน Mask mAP50-95 แต่การเลือกต้องพิจารณา inference และ pipeline แยกกัน
- Observation: YOLOv9e-Seg ใช้ peak allocated VRAM ต่ำสุด; จำนวน parameters ไม่ใช่ตัวแทน VRAM โดยตรง
- Observation: YOLO11x และ YOLOv9e มี Mask mAP50-95 ใกล้กันมาก
- Interpretation: ผลนี้ช่วยเลือก candidate for later CCTV robustness evaluation ยังไม่ใช่ข้อยืนยัน deployment

## Trade-off ที่เห็น

### Accuracy

YOLO26x-Seg มี Mask mAP50-95 สูงสุดในชุดนี้

### Speed

YOLOv9e-Seg มี inference mean ต่ำสุด ส่วน YOLOv9e-Seg มี pipeline mean ต่ำสุด; FPS ไม่รวม RLE preparation

### Memory / Resource

YOLOv9e-Seg มี peak allocated VRAM ต่ำสุด ต้องแยกจาก whole-device GPU memory

### ภาพรวม

เลือกตามข้อจำกัดจริง ไม่รวมเป็น weighted score และไม่อนุมานสาเหตุจาก architecture เพียงอย่างเดียว

## สิ่งที่ต้องระวังในการตีความ

ผลนี้เป็น Person instance segmentation รายเฟรมบน MOTS20 ไม่ใช่ MOTS tracking; TP-only IoU/Dice พิจารณาเฉพาะคู่ที่ match ได้ ภาพวิดีโอต่อเนื่องสัมพันธ์กันและไม่ได้ทดสอบ statistical significance ค่าใกล้กันควรอ่านว่า near-tied descriptively รุ่น E/X และ C/L ไม่ใช่ capacity เท่ากัน ผลยังไม่ยืนยัน blur, low-light, มุมกล้อง, ระดับ occlusion หรือความพร้อมใช้งาน CCTV; เป็น candidate for later CCTV robustness evaluation เท่านั้น

รอบ timing เดิมถูกตัดออก ใช้ clean repetitions ที่เก็บไว้เท่านั้น คงคำเตือน NNPACK และ pycocotools ตามหลักฐานเดิม

## ข้อมูลสำหรับนำไปรวมต่อ

[metrics/TIER_RESULTS.csv](metrics/TIER_RESULTS.csv) · [REPORT.md](REPORT.md) · [PRESENTATION_SUMMARY_TH.md](PRESENTATION_SUMMARY_TH.md) · [Master Study](https://github.com/folklazy/YOLO_Instance_Segmentation_MOTS20_Scaling_Study)
