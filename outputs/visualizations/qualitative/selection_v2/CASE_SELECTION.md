# Large — qualitative case selection v2

คัดจาก 12 frozen visualization frames โดยตรวจ per-frame metrics, original/GT และ saved RLE ที่ confidence ≥0.25 / mask matching IoU ≥0.50 ตาม evaluator/ignore policy เดิม ไม่รัน inference

1 shared anchor + 3 cases ตามพฤติกรรมของ tier ไม่บังคับภาพทั้งหมดตรงกันระหว่าง tier; ภายใน case ใช้เฟรมเต็มเดียวกันทุกโมเดล ROI เป็นภาพเสริม ไม่ซ่อน full-frame errors

| Case | Sequence / frame | Why selected / decision use | Source comparison |
|---|---|---|---|
| 1 | MOTS20-09 / 000525 | tier diagnostic: additional GT and fewer unmatched outputs; ใช้พิจารณา coverage ร่วมกับ extra masks: YOLO26x เก็บ 2003 โดยไม่มี FP แต่ YOLOv9e เก็บ 2004 ที่ YOLO26x พลาด แม้ทั้งคู่มี TP 7 เท่ากัน | new composite from saved predictions |
| 2 | MOTS20-09 / 000263 | shared anchor: common failure; ใช้ตั้งข้อจำกัดเมื่อความครบถ้วนของ Person ที่อยู่ระหว่างคนอื่นสำคัญ และตรวจการแยก instance ก่อนคัดโมเดล; ทุกโมเดลยังมีข้อผิดพลาด | reuse existing image |
| 3 | MOTS20-02 / 000600 | counterexample and near-tied pair; ช่วยตรวจคู่ near-tied YOLO11x/YOLOv9e: YOLO11x match 2029 ได้ แต่ YOLOv9e ไม่ได้; YOLOv8x เก็บครบแต่มี extra mask ริมขวา | reuse existing image |
| 4 | MOTS20-11 / 000450 | near-tied pair: same valid GT, different extra outputs; ใช้เทียบ YOLO11x/YOLOv9e ที่ mAP แทบเท่ากัน: ทั้งคู่เก็บ valid GT ครบ แต่ YOLOv9e มี FP สอง mask ขณะที่ YOLO11x ไม่มีในเฟรมนี้ | new composite from saved predictions |

## ทำไมบางภาพยังตรงกับ tier อื่น

Case 2 (09/263) ใช้ร่วมเพื่อเทียบ FN/FP บน GT ชุดเดียวกัน กรณีอื่นซ้ำได้เมื่อ error เดียวกันช่วยตรวจคนละโมเดล: 05/419 ใช้ L/M ตรวจ GT 2002; 02/1 ใช้ L/M ตรวจ equal counts และ GT ต่างชุด; 02/600 ใช้ Largest/Small ตรวจกรณีสวนอันดับ; 02/300 ใช้ Small/Nano ตรวจ TP–FP trade-off; 11/1 ใช้ L/N แต่ L ตรวจ GT 2016 ส่วน N ตรวจ GT 2028 และ extra mask; 11/450 ใช้ Largest/Medium ตรวจ coverage เท่ากันกับ extra output ของคนละชุดโมเดล ไม่ใช้จำนวนภาพซ้ำเป็นหลักฐานอิสระเพิ่ม

## การแทน case เดิม

เดิม Case 1 (05/419) แยก YOLOv8x ได้ แต่ไม่แยก YOLO26x/YOLO11x/YOLOv9e เท่ากรณีใหม่; เดิม Case 4 (09/1) TP 6 / FP 0 / FN 0 ทุกโมเดล จึงแทนด้วย coverage-control ที่มี extra output ต่างกัน ภาพ/หลักฐานเก่ายังคงเดิมเพื่อ audit; presentation เก่าเก็บใน reports/archive

## ขอบเขต

ทั้งห้า tier มี 20 case slots แต่ใช้ original frames ต่างกัน 10 เฟรม (เดิม 6) ชุดใหม่มี MOTS20-11 และยังมี common failure / counterexample ไม่เลือกเฉพาะ frame ที่ accuracy leader ชนะ ทั้งนี้ pool 12 เฟรมไม่แทน dataset; ไม่อ้างว่าเป็นเฟรมที่ต่างที่สุดใน 2,862 เฟรม ไม่ใช้ภาพวัด latency/VRAM หรือ statistical significance

[Candidate pool](CANDIDATE_POOL.json) · [Case evidence](CASE_EVIDENCE.json) · [Focus evidence](FOCUS_EVIDENCE.json) · [Decision audit](CASE_DECISION_AUDIT.json) · [Active selection](../../../../manifests/QUALITATIVE_SELECTION.json)
