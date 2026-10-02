# Largest (X/E)

## สรุปแบบกระชับ

- ทดสอบ YOLO26x-Seg, YOLO11x-Seg, YOLOv9e-Seg, YOLOv8x-Seg สำหรับ Person instance segmentation
- MOTS20 2,862 frames และ 26,894 Person GT instances เป็น annotation รายเฟรม ไม่ใช่จำนวนบุคคลไม่ซ้ำ
- ใช้ pretrained checkpoints / no fine-tuning ภายใต้ controlled benchmark เดียวกัน
- Accuracy สูงสุด: YOLO26x-Seg — Mask mAP50-95 0.603730
- Inference เร็วสุด: YOLOv9e-Seg; pipeline เร็วสุด: YOLOv9e-Seg
- Peak allocated VRAM ต่ำสุด: YOLOv9e-Seg
- ค่าความต่างเล็กมากเป็นเพียง near-tied descriptively ไม่ได้พิสูจน์ statistical significance
- คง PASS WITH WARNINGS และใช้ผลย้อนหลังเดิมทั้งหมด ไม่รัน inference ใหม่

## โมเดลที่ทดสอบ

1. YOLO26: `yolo26x-seg.pt`
2. YOLO11: `yolo11x-seg.pt`
3. YOLOv9: `yolov9e-seg.pt`
4. YOLOv8: `yolov8x-seg.pt`

## 1. ผลลัพธ์หลัก

YOLO26x-Seg มี Mask mAP50-95 สูงสุด 0.603730 ส่วน YOLOv9e-Seg มี inference mean ต่ำสุด และ YOLOv9e-Seg มี pipeline mean ต่ำสุด

YOLOv9e-Seg ใช้ peak allocated VRAM ต่ำสุด การเลือกจึงต้องแยก accuracy, เวลา forward, pipeline และ memory; ความต่างเล็กมากไม่ควรตีความเป็นความเหนือกว่าทางสถิติ

## 2. ผลรวมโมเดล

| Model | Mask mAP50-95 | AP50 | AP75 | Precision | Recall | F1 | TP-only IoU | TP-only Dice | Inference ms | Pipeline ms | FPS | Peak VRAM allocated MiB | Parameters |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| YOLO26x-Seg | 0.603730 | 0.903687 | 0.664426 | 0.946008 | 0.846285 | 0.893372 | 0.828873 | 0.902919 | 72.458 | 109.639 | 9.121 | 952.18 | 70,693,800 |
| YOLO11x-Seg | 0.536674 | 0.875806 | 0.575845 | 0.938702 | 0.822228 | 0.876613 | 0.801385 | 0.886046 | 69.406 | 105.885 | 9.444 | 942.48 | 62,142,656 |
| YOLOv9e-Seg | 0.536642 | 0.882037 | 0.572100 | 0.934230 | 0.826578 | 0.877113 | 0.799298 | 0.884605 | 65.888 | 103.376 | 9.673 | 855.41 | 60,512,800 |
| YOLOv8x-Seg | 0.524758 | 0.866402 | 0.560452 | 0.921598 | 0.814271 | 0.864616 | 0.798136 | 0.883841 | 67.843 | 109.441 | 9.137 | 1001.13 | 71,827,888 |


## 3. สรุปผลจากตาราง

### YOLO26x-Seg

อันดับเชิงตัวเลข: accuracy 1, inference speed 4, VRAM ต่ำ 3 จากโมเดลใน tier นี้ จุดเด่นคือ accuracy; จุดที่ด้อยกว่าคือ inference speed / VRAM เหมาะเป็นตัวเลือกเริ่มต้นเมื่อให้ความสำคัญกับ accuracy แต่ต้องตรวจ latency ตามข้อจำกัดจริง

### YOLO11x-Seg

อันดับเชิงตัวเลข: accuracy 2, inference speed 3, VRAM ต่ำ 2 จากโมเดลใน tier นี้ จุดเด่นคือ accuracy / VRAM; จุดที่ด้อยกว่าคือ inference speed ควรเปรียบเทียบกับตัวนำตามข้อจำกัดของงาน ไม่สรุปว่าลำดับที่ใกล้กันมีนัยสำคัญ

### YOLOv9e-Seg

อันดับเชิงตัวเลข: accuracy 3, inference speed 1, VRAM ต่ำ 1 จากโมเดลใน tier นี้ จุดเด่นคือ inference speed / VRAM; จุดที่ด้อยกว่าคือ accuracy เหมาะพิจารณาเมื่อจำกัดเวลา forward และยอมรับ accuracy ที่ต่ำกว่าตัวนำได้

### YOLOv8x-Seg

อันดับเชิงตัวเลข: accuracy 4, inference speed 2, VRAM ต่ำ 4 จากโมเดลใน tier นี้ จุดเด่นคือ inference speed; จุดที่ด้อยกว่าคือ accuracy / VRAM ควรเปรียบเทียบกับตัวนำตามข้อจำกัดของงาน ไม่สรุปว่าลำดับที่ใกล้กันมีนัยสำคัญ

## 4. Insight ที่สำคัญ

- Observation: YOLO26x-Seg นำด้าน Mask mAP50-95 แต่การเลือกต้องพิจารณา inference และ pipeline แยกกัน
- Observation: YOLOv9e-Seg ใช้ peak allocated VRAM ต่ำสุด; จำนวน parameters ไม่ใช่ตัวแทน VRAM โดยตรง
- Observation: YOLO11x และ YOLOv9e มี Mask mAP50-95 ใกล้กันมาก
- Interpretation: ผลนี้ช่วยเลือก candidate for later CCTV robustness evaluation ยังไม่ใช่ข้อยืนยัน deployment

## 5. Trade-off

### Accuracy

YOLO26x-Seg มี Mask mAP50-95 สูงสุดในชุดนี้

### Speed

YOLOv9e-Seg มี inference mean ต่ำสุด ส่วน YOLOv9e-Seg มี pipeline mean ต่ำสุด; FPS ไม่รวม RLE preparation

### Memory / Resource

YOLOv9e-Seg มี peak allocated VRAM ต่ำสุด ต้องแยกจาก whole-device GPU memory

### ภาพรวม

เลือกตามข้อจำกัดจริง ไม่รวมเป็น weighted score และไม่อนุมานสาเหตุจาก architecture เพียงอย่างเดียว

## 6. ถ้าต้องเลือกจาก Tier นี้

| Priority | Recommended model | Reason |
|---|---|---|
| Accuracy | YOLO26x-Seg | Mask mAP50-95 สูงสุด |
| Speed | YOLOv9e-Seg (inference); YOLOv9e-Seg (pipeline) | แยกตามส่วนที่เป็นข้อจำกัด |
| Low VRAM | YOLOv9e-Seg | peak allocated ต่ำสุด |
| Balanced trade-off | YOLO26x-Seg | เริ่มจาก accuracy สูงสุด แล้วตรวจว่ายอมรับ latency และ VRAM ได้; ไม่ใช่คะแนนรวม |


## 7. ข้อควรระวังในการตีความ

ผลนี้เป็น Person instance segmentation รายเฟรมบน MOTS20 ไม่ใช่ MOTS tracking; TP-only IoU/Dice พิจารณาเฉพาะคู่ที่ match ได้ ภาพวิดีโอต่อเนื่องสัมพันธ์กันและไม่ได้ทดสอบ statistical significance ค่าใกล้กันควรอ่านว่า near-tied descriptively รุ่น E/X และ C/L ไม่ใช่ capacity เท่ากัน ผลยังไม่ยืนยัน blur, low-light, มุมกล้อง, ระดับ occlusion หรือความพร้อมใช้งาน CCTV; เป็น candidate for later CCTV robustness evaluation เท่านั้น

คง PASS WITH WARNINGS; pipeline ไม่รวม RLE preparation และ disk I/O

## 8. สรุปสำหรับคุยกับพี่

- รอบนี้เทียบ Largest (X/E) ด้วย pretrained YOLO บน MOTS20 โดยใช้เงื่อนไขเดียวกัน
- ตัวนำด้าน accuracy คือ YOLO26x-Seg แต่ตัวที่ forward เร็วสุดคือ YOLOv9e-Seg
- ถ้าจำกัด VRAM ให้เริ่มพิจารณา YOLOv9e-Seg โดยดู accuracy ที่ยอมรับได้ประกอบ
- จุดที่ต้องระวังคือค่าที่ใกล้กันยังไม่ได้พิสูจน์นัยสำคัญ และ FPS ไม่ใช่ throughput ของระบบ CCTV เต็มรูปแบบ
- ขั้นถัดไปควรเติม tier ที่ยังไม่ทดสอบด้วย protocol เดิม หลังได้รับอนุมัติเท่านั้น

## รายละเอียดเต็ม

[REPORT.md](REPORT.md) · [metrics/TIER_RESULTS.csv](metrics/TIER_RESULTS.csv) · [Master Study](https://github.com/folklazy/YOLO_Instance_Segmentation_MOTS20_Scaling_Study)
