# election-69-OCR-result

Official 2026 Thai election results from the Election Commission of Thailand (กกต.), OCR-extracted from official Form สส.6/1 PDF announcements and structured as machine-readable JSON.

ผลคะแนนเลือกตั้ง 2569 อย่างเป็นทางการ แปลงจากแบบ สส.6/1 ที่ กกต. เผยแพร่เป็น PDF ให้อยู่ในรูปแบบ JSON

---

## ⚠️ Disclaimer

This dataset is produced through OCR processing with multi-model cross-validation using Google Cloud Vision API, Claude, Gemini, and other OCR engines and LLMs to ensure accuracy before publishing. We do not alter, modify, or manipulate any election data in any way.

This is an independent volunteer civic effort to help digitize official election results published by the Election Commission of Thailand (กกต.), which we believe may lack sufficient resources to do so at scale. All processing costs are self-funded by the author personally — this project has no affiliation with any business, political party, or civic organization whatsoever.

For official and authoritative results, please always refer to the original documents from กกต.

## ⚠️ ข้อสงวนสิทธิ์

ข้อมูลชุดนี้ถูกสร้างจากการอ่าน OCR โดยผ่านการตรวจสอบความถูกต้องข้ามระบบ (cross-validation) ด้วย Google Cloud Vision API, Claude, Gemini และ OCR engine และ LLM อื่นๆ เพื่อความแม่นยำก่อนเผยแพร่ เราไม่มีส่วนเกี่ยวข้องในการแก้ไข ดัดแปลง หรือบิดเบือนข้อมูลผลการเลือกตั้งใดๆ ทั้งสิ้น

โครงการนี้จัดทำขึ้นโดยสมัครใจเพื่อช่วย กกต. ในการ digitize ผลการเลือกตั้งที่เผยแพร่อย่างเป็นทางการ ซึ่งเราเชื่อว่า กกต. อาจมีทรัพยากรไม่เพียงพอในการดำเนินการด้วยตนเอง ค่าใช้จ่ายในการประมวลผลทั้งหมดเป็นทุนส่วนตัวของผู้จัดทำ — โครงการนี้ไม่มีความเกี่ยวข้องกับธุรกิจ พรรคการเมือง หรือองค์กรภาคประชาสังคมใดๆ ทั้งสิ้น

สำหรับผลการเลือกตั้งที่เป็นทางการ กรุณาอ้างอิงจากเอกสารต้นฉบับของ กกต. เสมอ

---

## 📊 Data Coverage / ความครอบคลุมของข้อมูล

ประมวลผลจาก **776 PDF scans** (แบบ สส.6/1 สแกนจากเครื่อง Canon ไม่มี text layer) จาก กกต. → Gemini Vision OCR → structured JSON **773 files**

|  | สส.เขต (Constituency) | บัญชีรายชื่อ (Party List) |
|---|---|---|
| **เขตที่นำเข้าแล้ว** | 387 / 400 (96.8%) | 386 / 400 (96.5%) |
| **Vote sum mismatches** | 0 | 0 |
| **Duplicate candidates** | 0 | N/A |
| **Data consistency** | ✓ (area = province = national) | ✓ (area = province = national) |

### ตัวเลขสำคัญ — Final Result

|  | สส.เขต (Constituency) | บัญชีรายชื่อ (Party List) |
|---|---|---|
| **คะแนนรวม (total votes)** | 33,819,647 | 33,903,675 |
| **ผู้มีสิทธิเลือกตั้ง (eligible voters)** | 51,263,889 | 51,175,456 |

### แบบบัญชีรายชื่อ (Party List) — Top 5

| พรรค | คะแนน |
|------|-------|
| ประชาชน | 10,715,927 |
| ภูมิใจไทย | 5,967,124 |
| เพื่อไทย | 5,376,290 |
| ประชาธิปัตย์ | 3,910,896 |
| เศรษฐกิจ | 1,109,392 |
| **รวมทุกพรรค** | **33,903,675** |

---

## 📂 Data Structure / โครงสร้างข้อมูล

```
data/
├── csv/                            # CSV รวม — เปิดได้ด้วย Excel / Google Sheets
│   ├── constituency.csv            # ผลแบบแบ่งเขต ทุกผู้สมัคร (3,370 rows)
│   ├── party_list.csv              # ผลแบบบัญชีรายชื่อ ทุกพรรค (22,008 rows)
│   └── summary_winners.csv        # สรุปผู้ชนะแบบแบ่งเขต (387 rows)
├── matched/                        # JSON ที่ผ่าน validation + matched กับฐานข้อมูลผู้สมัคร
│   ├── constituency/               # แบบแบ่งเขต (387 files)
│   ├── party_list/                 # แบบบัญชีรายชื่อ (386 files)
│   ├── issues.json                 # รายการปัญหาที่พบ
│   └── validation_report.json      # สรุปผลการตรวจสอบ
└── ocr-output/                     # JSON ดิบจาก OCR
    ├── constituency/               # แบบแบ่งเขต (387 files)
    └── party_list/                 # แบบบัญชีรายชื่อ (386 files)
```

### CSV Files (สำหรับเปิดด้วย Excel / Google Sheets)

| ไฟล์ | คำอธิบาย | คอลัมน์ |
|------|----------|---------|
| `constituency.csv` | ผลคะแนนแบบแบ่งเขต ทุกผู้สมัคร | รหัสจังหวัด, จังหวัด, เขต, หมายเลข, ชื่อผู้สมัคร, พรรค, คะแนน |
| `party_list.csv` | ผลคะแนนแบบบัญชีรายชื่อ ทุกพรรค | รหัสจังหวัด, จังหวัด, เขต, หมายเลข, พรรค, คะแนน |
| `summary_winners.csv` | สรุปผู้ชนะแบบแบ่งเขต | รหัสจังหวัด, จังหวัด, เขต, ผู้ชนะ, พรรค, คะแนน, คะแนนดี, ผู้มีสิทธิ, มาใช้สิทธิ |

### Matched JSON (แนะนำสำหรับนักพัฒนา)

ข้อมูลที่ผ่านการ validate และ match กับฐานข้อมูลผู้สมัครแล้ว มีข้อมูลเพิ่มเติม:

- `province_code` — รหัสจังหวัด
- `summary` — สรุปภาพรวม (eligible_voters, good_votes, invalid_votes, ฯลฯ)
- `matched_candidates` — ผู้สมัครที่ match ได้พร้อม `candidate_uuid`
- `unmatched_candidates` — ผู้สมัครที่ match ไม่ได้
- `issues.json` — รายการปัญหาที่พบระหว่าง validation
- `validation_report.json` — สรุปผลการตรวจสอบทั้งหมด

### Raw OCR JSON (ข้อมูลดิบ)

- **ocr-output/constituency/** — ผลคะแนนแบบแบ่งเขตเลือกตั้ง (387 files)
- **ocr-output/party_list/** — ผลคะแนนแบบบัญชีรายชื่อ (386 files)

---

## 🔍 Quality Assurance / การตรวจสอบคุณภาพ

### บัญชีรายชื่อ (Party List) — 15 เขตที่ vote sum ไม่ตรง

แก้ไขทั้งหมดแล้ว → **0 mismatches**

| ประเภทปัญหา | จำนวน | ตัวอย่าง |
|-------------|-------|----------|
| Phantom/hallucinated entries | 10 areas | Gemini แทรก "Unknown Party" เปล่าๆ ดันพรรคจริงหลุด |
| Missing parties | 7 areas | พรรคหายไปเพราะ phantom เข้ามาแทนที่ เช่น ใหม่, รวมใจไทย, ไทยทรัพย์ทวี |
| Thai numeral misreads | 3 areas | ๖→๕, ๐↔๒ transposition, ๘→๔ |

> แก้โดยเทียบกับ PDF ต้นฉบับทีละเขต

### สส.เขต (Constituency) — 45 เขตที่เลขผู้สมัครซ้ำ

แก้ไขทั้งหมดแล้ว → **0 duplicates**

- Gemini อ่านเลขหมายผู้สมัครผิด/สลับ/ซ้ำกัน
- แก้โดย query ข้อมูลจริงจาก Reporter DB แล้ว match ด้วยชื่อพรรค

### Remaining Known Issues

- **35 unmatched party entries** — phantom/blank entries (0 votes) ไม่กระทบตัวเลขรวม
- **2 unmatched candidates** — ถูกถอนชื่อ/ชื่อไม่ตรง DB

---

## 🚫 Missing Areas / เขตที่ยังไม่มีข้อมูล

### กกต. ยังไม่ประกาศผล 3 เขต

| จังหวัด | เขต | สถานะ |
|---------|------|--------|
| กรุงเทพมหานคร | เขตเลือกตั้งที่ 15 | กกต. ยังไม่ประกาศผล |
| น่าน | เขตเลือกตั้งที่ 1 | กกต. ยังไม่ประกาศผล |
| อุดรธานี | เขตเลือกตั้งที่ 6 | กกต. ยังไม่ประกาศผล |

> ดูประกาศต้นฉบับ: [`assets/ect-announcement.jpeg`](assets/ect-announcement.jpeg)

### สส.เขต (Constituency) — ขาด 13 เขต

| # | จังหวัด | เขต | หมายเหตุ |
|---|---------|------|----------|
| 1 | กรุงเทพมหานคร | 15 | กกต. ยังไม่ประกาศ |
| 2 | น่าน | 1 | กกต. ยังไม่ประกาศ |
| 3 | บุรีรัมย์ | 1 | ไม่มี PDF จาก กกต. |
| 4 | บุรีรัมย์ | 2 | ไม่มี PDF จาก กกต. |
| 5 | บุรีรัมย์ | 3 | ไม่มี PDF จาก กกต. |
| 6 | บุรีรัมย์ | 4 | ไม่มี PDF จาก กกต. |
| 7 | บุรีรัมย์ | 5 | ไม่มี PDF จาก กกต. |
| 8 | บุรีรัมย์ | 6 | ไม่มี PDF จาก กกต. |
| 9 | บุรีรัมย์ | 7 | ไม่มี PDF จาก กกต. |
| 10 | บุรีรัมย์ | 8 | ไม่มี PDF จาก กกต. |
| 11 | บุรีรัมย์ | 9 | ไม่มี PDF จาก กกต. |
| 12 | บุรีรัมย์ | 10 | ไม่มี PDF จาก กกต. |
| 13 | ปราจีนบุรี | 2 | |

### บัญชีรายชื่อ (Party List) — ขาด 14 เขต

| # | จังหวัด | เขต | หมายเหตุ |
|---|---------|------|----------|
| 1 | กรุงเทพมหานคร | 15 | กกต. ยังไม่ประกาศ |
| 2 | นครพนม | 2 | |
| 3 | บุรีรัมย์ | 1 | ไม่มี PDF จาก กกต. |
| 4 | บุรีรัมย์ | 2 | ไม่มี PDF จาก กกต. |
| 5 | บุรีรัมย์ | 3 | ไม่มี PDF จาก กกต. |
| 6 | บุรีรัมย์ | 4 | ไม่มี PDF จาก กกต. |
| 7 | บุรีรัมย์ | 5 | ไม่มี PDF จาก กกต. |
| 8 | บุรีรัมย์ | 6 | ไม่มี PDF จาก กกต. |
| 9 | บุรีรัมย์ | 7 | ไม่มี PDF จาก กกต. |
| 10 | บุรีรัมย์ | 8 | ไม่มี PDF จาก กกต. |
| 11 | บุรีรัมย์ | 9 | ไม่มี PDF จาก กกต. |
| 12 | บุรีรัมย์ | 10 | ไม่มี PDF จาก กกต. |
| 13 | ปราจีนบุรี | 2 | |
| 14 | อุดรธานี | 6 | กกต. ยังไม่ประกาศ |

---

## 📅 Timeline

| วันที่ | เหตุการณ์ |
|-------|----------|
| 2026-02-08 (8 ก.พ. 69) | วันเลือกตั้ง สส. 2569 |
| 2026-02-20 (20 ก.พ. 69) | กกต. ประกาศผลการนับคะแนนอย่างเป็นทางการ 100% เป็น PDF (776 ไฟล์) ยกเว้น 3 เขต |
| 2026-02-20 (20 ก.พ. 69) | เริ่มประมวลผล OCR จาก 776 PDF scans |
| 2026-02-21 (21 ก.พ. 69) | นำเข้าข้อมูล matched: สส.เขต 387/400, บัญชีรายชื่อ 386/400 |
| 2026-02-21 (21 ก.พ. 69) | แก้ไข 15 OCR errors บัญชีรายชื่อ (phantom entries, missing parties, digit misreads) — vote sum mismatch = 0 |
| 2026-02-21 (21 ก.พ. 69) | แก้ไขเลขผู้สมัครซ้ำ 45 เขต สส.เขต — duplicate candidates = 0 |

> Timeline จะอัปเดตเมื่อ กกต. ประกาศผลเพิ่มเติม หรือเมื่อข้อมูลได้รับการแก้ไข

---

## 📌 Attribution / การอ้างอิง

If you use this dataset, please credit:

**ชานนท์ เงินทองดี (Chanon Ngernthongdee)**

or link back to this repository: [election-69-OCR-result](https://github.com/killernay/election-69-OCR-result)

หากนำข้อมูลชุดนี้ไปใช้ กรุณาให้เครดิต **นายชานนท์ เงินทองดี** หรืออ้างอิงกลับมาที่ repository นี้

---

## 🐛 Found an Error? / พบข้อผิดพลาด?

If you find any inaccuracies in the data, please report via:

**Twitter/X:** [@killernay](https://x.com/killernay)

หากพบข้อผิดพลาดในข้อมูล สามารถแจ้งได้ที่ [@killernay](https://x.com/killernay) บน Twitter/X — หากว่างจะรีบตรวจสอบและแก้ไขทันที

---

## 📄 Data Source / แหล่งข้อมูลต้นฉบับ

- แบบ สส.6/1 จากสำนักงานคณะกรรมการการเลือกตั้ง (กกต.)
- [https://www.ect.go.th](https://www.ect.go.th)

![ประกาศ กกต.](assets/ect-announcement.jpeg)

## 🛠️ Processing Pipeline

```
776 PDF scans (กกต. — Canon copier, no text layer)
    │
    ▼
┌──────────────────┐     ┌──────────────────────┐
│  Gemini Vision   │     │  ฐานข้อมูลอ้างอิง      │
│  OCR + LLM       │     │  - อาสาสมัครวันเลือกตั้ง │
│                  │     │  - เว็บไม่เป็นทางการ กกต. │
└────────┬─────────┘     └───────────┬──────────┘
         │                           │
         ▼                           │
┌──────────────────┐                 │
│  Validate + Match │◄────────────────┘
│  Vote sum check   │
│  Candidate UUIDs  │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│  Fix OCR Errors   │
│  Party list (15)  │
│  Candidate # (45) │
└────────┬─────────┘
         │
         ▼
   JSON + CSV output
   (raw + matched)
```

1. **Source** — 776 PDF scans (แบบ สส.6/1) จาก กกต. สแกนจากเครื่อง Canon ไม่มี text layer ต้อง OCR ทั้งหมด
2. **OCR** — Gemini Vision เป็นหลัก + cross-validation กับ Google Cloud Vision API, Claude และ OCR engine/LLM อื่นๆ
3. **Validate + Match** — ตรวจ vote sums, match province codes + candidate/party UUIDs, เทียบกับฐานข้อมูลอาสาสมัครวันเลือกตั้ง และเว็บไม่เป็นทางการของ กกต.
4. **Fix OCR Errors** — แก้ party list 15 ไฟล์ (phantom entries, digit misreads) + แก้เลขผู้สมัครซ้ำ 45 ไฟล์ สส.เขต
5. **Output** — JSON (raw 773 files + matched 773 files) และ CSV

## 📜 License

This data is derived from publicly available official government documents. The structured JSON output is provided freely for public use. Please attribute as noted above.
