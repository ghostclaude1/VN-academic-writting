# VN-academic-writing

**Kỹ năng viết học thuật tiếng Việt cho ĐATN** — văn phong chuẩn paper VN, anti-AI detection, thuật ngữ chuyên ngành, IEEE citation.

Được xây dựng riêng cho đề tài:
> *"Xây dựng nền tảng quản lý danh sách theo dõi và cảnh báo giao dịch bất thường trong phiên cho cổ phiếu VN30"*

---

## Cài đặt nhanh (cho session mới)


```
1. Truy cập thư mục skills/
2. chạy `git clone https://github.com/ghostclaude1/VN-academic-writting.git` để cài trong thư mục skills
3. Đăng ký vào AGENTS.md
```

###  Đăng ký vào AGENTS.md

Thêm vào bảng Skills trong `AGENTS.md`:

```markdown
| VN-academic-writing | `skills/VN-academic-writing/SKILL.md` | Viết học thuật tiếng Việt cho ĐATN — văn phong chuẩn paper VN, anti-AI detection, thuật ngữ chuyên ngành, IEEE citation. Kèm đầy đủ context đề tài VN30 anomaly detection. |
```

---

## Cấu trúc thư mục

```
skills/VN-academic-writing/
├── README.md                       ← file này
├── SKILL.md                        ← entry point (v2.3) — đọc trước khi viết
├── ĐATN-academic-writing.md        ← bộ quy tắc đầy đủ
├── mega-rule-v2.md                 ← context kỹ thuật + tech stack
├── beWritten.md                    ← bản viết thực tế (cập nhật liên tục)
├── references.md                   ← 25+ papers, IEEE format
├── paper_analysis.md               ← phân tích chuyên sâu 5 papers
├── new_papers_to_review.md         ← 17 papers mới đã verify
└── papers/                         ← 22 PDFs
    ├── liu2008_isolation_forest.pdf
    ├── ding2013_iForestASD.pdf
    ├── togbe2021_IF_concept_drift.pdf
    ├── hariri2021_EIF.pdf
    ├── guha2016_RRCF.pdf
    ├── poutre2024_hfm_anomaly.pdf
    ├── nunez2024_kpartitioned_IF.pdf
    ├── yang2025_LSTM_GAN.pdf
    ├── huynh2024_VN_AD.pdf
    ├── bakumenko2022_IF_financial.pdf
    ├── cont2014_OFI_price_impact.pdf
    ├── cont2023_cross_OFI.pdf
    ├── anantha2024_HF_OFI.pdf
    ├── zarattini2023_VWAP.pdf
    ├── carcillo2018_SCARFF.pdf
    ├── bhatia2022_memstream.pdf
    ├── le_hoang_anh2024_VN1.pdf
    ├── phuoc2024_ML_VN_stock.pdf
    ├── idan2024_unsupervised_validation.pdf
    ├── darban2024_DL_TS_AD_survey.pdf
    ├── pang2021_DL_AD_review.pdf
    └── park2024_LLM_AD_financial.pdf
```

---

## Cách dùng khi viết

**Mỗi lần bắt đầu viết một section mới:**

```
1. Đọc SKILL.md (entry point, nguyên tắc tổng quát)
2. Đọc ĐATN-academic-writing.md § phần tương ứng (cấu trúc, ví dụ)
3. Đọc mega-rule-v2.md nếu cần tra số liệu kỹ thuật
4. Đọc beWritten.md để bắt kịp giọng văn và citation numbers đang dùng
5. Đọc trực tiếp PDF papers liên quan trước khi trích dẫn
6. Viết → chạy checklist § 3.6 của SKILL.md trước khi submit
7. Cập nhật beWritten.md sau khi section được duyệt
```

**Tra citation number:** Xem `beWritten.md` — các số [N] đã dùng được ghi rõ trong context.

**Tra thuật ngữ:** `SKILL.md` § IV hoặc `ĐATN-academic-writing.md` § Phần IV.

**Cần đọc paper:** Dùng `sandbox-mcp.file_read` với path `skills/VN-academic-writing/papers/<tên_file>.pdf`.

---

## Tích hợp với ARS

Skill này **xếp chồng lên** ARS academic-paper pipeline:

| ARS Phase | VN-academic-writing bổ sung |
|-----------|----------------------------|
| Phase 0: CONFIG | IEEE citation format cho ĐATN kỹ thuật VN |
| Phase 4: DRAFTING | Văn phong VN chuẩn, anti-AI patterns, burstiness |
| Phase 6: PEER REVIEW | Checklist §3.6 — kiểm tra AI-isms tiếng Việt |
| Phase 7: FORMAT | Chuẩn số VND, phần trăm, năm theo chuẩn VN |

ARS path: `skills/ars/academic-paper/SKILL.md`

---

## Papers theo nhóm

| Nhóm | Papers | Mã file |
|------|--------|---------|
| **A — Isolation Forest** | Liu 2008, Hariri 2021, Ding 2013, Togbe 2021, Guha 2016 | `liu2008_*`, `hariri2021_*`, `ding2013_*`, `togbe2021_*`, `guha2016_*` |
| **B — AD tài chính** | Poutré 2024, Núñez 2024, Yang 2025, Huynh 2024, Bakumenko 2022 | `poutre2024_*`, `nunez2024_*`, `yang2025_*`, `huynh2024_*`, `bakumenko2022_*` |
| **C — OFI & Microstructure** | Cont 2014, Cont 2023, Anantha 2024 | `cont2014_*`, `cont2023_*`, `anantha2024_*` |
| **D — VWAP** | Zarattini 2023 | `zarattini2023_*` |
| **E — Streaming pipeline** | Carcillo 2018, Bhatia 2022 | `carcillo2018_*`, `bhatia2022_*` |
| **F — Thị trường VN** | Lê Hoàng Anh 2024, Phuoc 2024 | `le_hoang_anh2024_*`, `phuoc2024_*` |
| **G — Đánh giá unsupervised** | Idan 2024 | `idan2024_*` |
| **H — Survey** | Darban 2024, Pang 2021, Park 2024 | `darban2024_*`, `pang2021_*`, `park2024_*` |

---

## Trạng thái hiện tại

| Phần báo cáo | Trạng thái |
|-------------|-----------|
| MỞ ĐẦU | ✅ Hoàn thành |
| §1.1 Đặt vấn đề | ✅ Hoàn thành |
| §1.2.1 Nghiên cứu thế giới | ✅ Hoàn thành |
| §1.2.2 Nghiên cứu trong nước | ✅ Hoàn thành |
| §1.2.3 Khoảng trống nghiên cứu | ✅ Hoàn thành |
| §1.3 Mục tiêu | ⏳ Chờ viết |
| §1.4 Phạm vi | ⏳ Chờ viết |
| §1.5 Tổng kết chương 1 | ⏳ Chờ viết |
| Chương 2 | ⏳ Chưa bắt đầu |
| Chương 3 | ⏳ Chưa bắt đầu |
| Chương 4 | ⏳ Chưa bắt đầu |

> **Cập nhật bảng này** sau mỗi section được duyệt.

---

## Lịch sử cài đặt

| Ngày | Thao tác |
|------|---------|
| 2026-05-15 | Tạo skill, upload 7 file cốt lõi |
| 2026-05-15 | Upload 22 PDFs vào `papers/` |
| 2026-05-15 | Tạo README.md này |

---
