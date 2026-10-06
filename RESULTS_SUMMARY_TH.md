# สรุปผล Largest (X/E) YOLO Instance Segmentation

## สรุปใน 1 นาที

- โมเดล: YOLO26x-Seg, YOLO11x-Seg, YOLOv9e-Seg, YOLOv8x-Seg
- MOTS20 2,862 เฟรม / 26,894 Person GT รายเฟรม (annotation รายเฟรม)
- Official pretrained checkpoints / ไม่ปรับจูน; สถานะเดิม PASS WITH WARNINGS
- ความแม่นยำสูงสุด: YOLO26x-Seg — Mask mAP50-95 0.603730
- เร็วสุด: inference YOLOv9e-Seg (65.888 ms); pipeline YOLOv9e-Seg (103.376 ms)
- Peak allocated VRAM ต่ำสุด: YOLOv9e-Seg — 855.41 MiB
- Trade-off หลัก: YOLO26x-Seg นำรองอันดับสอง 6.705603 percentage points ของ mAP; เวลา inference มากกว่าตัวเร็วสุด 6.570 ms

## ผลลัพธ์หลัก

| โมเดล | Mask mAP50-95 | AP75 | Recall | Inference (ms) | Pipeline (ms) | FPS | Peak allocated VRAM (MiB) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| YOLO26x-Seg | 0.603730 | 0.664426 | 0.846285 | 72.458 | 109.639 | 9.121 | 952.18 |
| YOLO11x-Seg | 0.536674 | 0.575845 | 0.822228 | 69.406 | 105.885 | 9.444 | 942.48 |
| YOLOv9e-Seg | 0.536642 | 0.572100 | 0.826578 | 65.888 | 103.376 | 9.673 | 855.41 |
| YOLOv8x-Seg | 0.524758 | 0.560452 | 0.814271 | 67.843 | 109.441 | 9.137 | 1001.13 |

## สรุปผลจากตาราง

อ่านร่วมกับตารางหลักด้านบน; AP50 และ TP-only IoU/Dice อ้างอิง [CSV มาตรฐาน](metrics/TIER_RESULTS.csv) และ [REPORT.md](REPORT.md) ตัวเลข TP-only วัดเฉพาะคู่ที่ จับคู่ ได้ จึงไม่แทนความครอบคลุม GT หรือคุณภาพทุก instance

### YOLO26x-Seg

นำทั้ง AP50, AP75, mAP50-95 และ Recall รวมถึง TP-only IoU/Dice จึงมีหลักฐานหลายด้านว่าครอบคลุม GT ได้มากกว่าและมี mask overlap เฉลี่ยสูงกว่าในชุดนี้ Recall 84.63% ยังเหลือ GT ที่พลาดหรือจับคู่ไม่ผ่าน; ส่วน TP-only quality ไม่ครอบคลุมคนที่พลาดและไม่ได้เปรียบเทียบคู่ GT ชุดเดียวกันระหว่างโมเดล

สิ่งที่แลกคือ inference 72.458 ms ซึ่งช้าที่สุดในกลุ่มและ allocated VRAM 952.18 MiB สูงกว่า YOLOv9e แต่ไม่สูงสุด หากยอมรับเวลาแฝงเพิ่มเพื่อ accuracy รุ่นนี้เป็นตัวเลือกนำไปทดลองต่อ โดยต้องพิจารณา pipeline 109.639 ms ด้วย

### YOLO11x-Seg

mAP แทบเท่า YOLOv9e แต่ AP75 และ TP-only IoU/Dice สูงกว่าเล็กน้อย ขณะที่ Recall ต่ำกว่าและทั้ง inference/pipeline ช้ากว่า จึงไม่ควรเรียกว่า “สมดุลดีที่สุด” โดยอัตโนมัติ ความต่าง mAP ระดับทศนิยมท้ายไม่ใช่หลักฐาน statistical superiority

เป็นคู่เปรียบเทียบที่มีประโยชน์เมื่อต้องการแยกคุณภาพ mask ของคู่ที่ จับคู่ ได้ออกจากความครอบคลุม GT; การเลือกเหนือ YOLOv9e ต้องมีเหตุผลจากข้อจำกัดงานหรือข้อมูลเพิ่มเติม เพราะรอบนี้ใช้ VRAM 942.48 MiB มากกว่าและยังไม่มีการทดสอบความมีนัยสำคัญ

### YOLOv9e-Seg

เด่นด้านทรัพยากร: inference 65.888 ms และ pipeline 103.376 ms เร็วสุด พร้อม peak allocated VRAM 855.41 MiB ต่ำสุด โดย mAP แทบเท่า YOLO11x จึงไม่ได้ลด mAP มากเมื่อเทียบคู่นี้ อีกทั้ง Recall สูงกว่า YOLO11x เล็กน้อย แต่ AP75 และ TP-only quality ต่ำกว่าเล็กน้อย

อย่างไรก็ตาม mAP/AP75 ยังต่ำกว่า YOLO26x ตามค่าที่วัด เหมาะเป็นตัวเลือกเมื่อเวลาแฝง/VRAM เป็นข้อจำกัดหลัก โดยไม่ถือว่าเป็นผู้ชนะด้าน accuracy หรือทุกด้านพร้อมกัน

### YOLOv8x-Seg

mAP ต่ำสุดและ allocated VRAM 1001.13 MiB สูงสุดในสี่รุ่น แม้ inference 67.843 ms เร็วกว่า YOLO11x และ YOLO26x แต่ pipeline 109.441 ms อยู่ใกล้ YOLO26x และช้ากว่า YOLOv9e จึงไม่ควรใช้ forward เวลาแฝงเพียงค่าเดียวเป็นเหตุผลเลือก

จากค่าที่วัด YOLOv9e มี mAP สูงกว่า พร้อม inference/pipeline เร็วกว่าและใช้ VRAM ต่ำกว่า จึงเป็นคู่ที่ควรพิจารณาก่อนภายใต้ข้อจำกัดเหล่านี้ ส่วน YOLOv8x ยังใช้เป็น baseline รุ่นก่อนเพื่อทดลองต่อได้ ผลนี้ไม่พิสูจน์สาเหตุจากโครงสร้างโมเดลเพราะ capacity/checkpoint/pretraining ต่างกัน

## ผู้ชนะในแต่ละด้าน

| ด้าน | โมเดล | ผลลัพธ์ |
| --- | --- | --- |
| Mask mAP50-95 | YOLO26x-Seg | 0.603730 |
| AP75 | YOLO26x-Seg | 0.664426 |
| Recall | YOLO26x-Seg | 0.846285 |
| Inference เร็วสุด | YOLOv9e-Seg | 65.888 ms |
| Pipeline เร็วสุด | YOLOv9e-Seg | 103.376 ms |
| VRAM | YOLOv9e-Seg | 855.41 MiB |

## สิ่งที่ตัวเลขบอกเรา

- mAP ของ YOLO26x-Seg สูงกว่า YOLO11x-Seg 6.705603 percentage points
- YOLO11x และ YOLOv9e มี mAP ต่างกันเพียง 0.000032 (0.003190 percentage points); เป็น descriptive คะแนนใกล้กัน
- YOLOv8x มี peak VRAM สูงสุด 1001.13 MiB แต่ mAP ต่ำสุดในขนาด
- ความแม่นยำ winner ใช้ VRAM มากกว่าตัวต่ำสุด 96.78 MiB; การจัดอันดับ inference และ pipeline ต้องแยกกัน

## ข้อแลกเปลี่ยนหลัก

### ความแม่นยำกับความเร็ว

YOLO26x-Seg มี mAP 0.603730; YOLOv9e-Seg มี mAP 0.536642
และ inference 65.888 ms เทียบกับ 72.458 ms ของโมเดลนำด้านความแม่นยำ
Pipeline winner คือ YOLOv9e-Seg (103.376 ms); ไม่ใช้เวลา forward แทน throughput ของ pipeline

### ความแม่นยำกับหน่วยความจำ

YOLO26x-Seg ใช้ 952.18 MiB; YOLOv9e-Seg ใช้ 855.41 MiB
และมี mAP 0.536642

## ข้อควรระวังในการตีความ

ไม่มีการทดสอบนัยสำคัญทางสถิติ; คะแนนใกล้กันเป็นคำบรรยาย ค่า AP/Recall อยู่ช่วง 0–1
Pipeline ไม่รวม RLE preparation และการอ่านเขียนดิสก์; VRAM เป็น peak allocated
MOTS20 ไม่ใช่ผลทดสอบความทนทานต่อ CCTV ขั้นสุดท้ายและ E/X, C/L ไม่ใช่ capacity เท่ากัน

## ข้อมูลสำหรับนำไปรวมต่อ

นำ YOLO26x สำหรับ accuracy และ YOLOv9e สำหรับ speed/VRAM; เก็บ YOLO11x เป็นคู่คะแนนใกล้กันของ YOLOv9e ไปเทียบข้ามขนาดโดยคง protocol และแหล่ง canonical เดิม ยังไม่สรุปครบ 17 โมเดล

[TIER_RESULTS.csv](metrics/TIER_RESULTS.csv) · [REPORT.md](REPORT.md) ·
[การวิเคราะห์ภาพ](PRESENTATION_SUMMARY_TH.md) ·
[การศึกษาหลัก](https://github.com/folklazy/YOLO_Instance_Segmentation_MOTS20_Scaling_Study)
