# Largest (X/E) — การทดสอบ YOLO Instance Segmentation บน MOTS20

## ภาพรวม

เปรียบเทียบการแยก Person เป็นราย instance บน MOTS20 ด้วยโมเดล pretrained โดยไม่ฝึกเพิ่มหรือปรับจูน ประเมินรายเฟรมไม่ใช่การติดตามคน เอกสารนี้ใช้แนะนำ repository และเชื่อมไปยังผลเชิงตัวเลขรายงานเทคนิคและการวิเคราะห์ภาพ

## โมเดลที่ทดสอบ

| ตระกูล | โมเดล | ขนาด |
| --- | --- | --- |
| YOLO26 | YOLO26x-Seg | Largest (X/E) |
| YOLO11 | YOLO11x-Seg | Largest (X/E) |
| YOLOv9 | YOLOv9e-Seg | Largest (X/E) |
| YOLOv8 | YOLOv8x-Seg | Largest (X/E) |

## สถานะการทดลอง

COMPLETE / PASS WITH WARNINGS — ครบ 4/4 โมเดล โมเดลละ 2,862 เฟรมและ Person GT รายเฟรม 26,894 instances
รอบทดลอง: `benchmark-20260929T0520Z` ใช้ผลที่บันทึกไว้ ไม่มีการรัน inference ใหม่เพื่อปรับเอกสาร

## ผลลัพธ์หลัก

| โมเดล | Mask mAP50-95 | Recall | F1 | Inference (ms) | Pipeline (ms) | FPS | Peak allocated VRAM (MiB) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| YOLO26x-Seg | 0.603730 | 0.846285 | 0.893372 | 72.458 | 109.639 | 9.121 | 952.18 |
| YOLO11x-Seg | 0.536674 | 0.822228 | 0.876613 | 69.406 | 105.885 | 9.444 | 942.48 |
| YOLOv9e-Seg | 0.536642 | 0.826578 | 0.877113 | 65.888 | 103.376 | 9.673 | 855.41 |
| YOLOv8x-Seg | 0.524758 | 0.814271 | 0.864616 | 67.843 | 109.441 | 9.137 | 1001.13 |

## เอกสารประกอบ

- [บทสรุปเชิงตัวเลข](RESULTS_SUMMARY_TH.md)
- [การวิเคราะห์ภาพและพฤติกรรมเชิงคุณภาพ](PRESENTATION_SUMMARY_TH.md)
- [รายงานเทคนิค](REPORT.md)
- [โพรโทคอลการทดลอง](EXPERIMENT_PROTOCOL.md)

## การนำทางในชุดการศึกษา

[Largest (X/E)](https://github.com/folklazy/YOLO_Large_Seg_MOTS20_Benchmark) | [Second-largest (L/C)](https://github.com/folklazy/YOLO_Second_Largest_Seg_MOTS20_Benchmark) | [Medium (M)](https://github.com/folklazy/YOLO_Medium_Seg_MOTS20_Benchmark) | [Small (S)](https://github.com/folklazy/YOLO_Small_Seg_MOTS20_Benchmark) | [Nano (N)](https://github.com/folklazy/YOLO_Nano_Seg_MOTS20_Benchmark) | [การศึกษาหลัก](https://github.com/folklazy/YOLO_Instance_Segmentation_MOTS20_Scaling_Study)

## หลักฐานสำหรับตรวจสอบซ้ำ

[ค่าตัวชี้วัด](metrics/) · [การตั้งค่า](configs/) · [หลักฐานและแหล่งที่มา](manifests/) · [ภาพและกราฟ](outputs/) · [บันทึกย้อนหลัง](reports/archive/)

[บทตีความจากรอบเดิม](BENCHMARK_INSIGHTS_TH.md) เป็นบันทึกย้อนหลัง เก็บภาษาตามต้นฉบับ; บทสรุปปัจจุบันใช้เอกสารด้านบน
