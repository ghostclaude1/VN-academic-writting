---
name: vn-academic-writing
description: "Kỹ năng viết học thuật tiếng Việt cho ĐATN, kết hợp với ARS academic-paper pipeline. Ưu tiên học từ paper tiếng Việt là nguồn chuẩn về thuật ngữ và lối hành văn. Bao gồm: văn phong academic VN chuẩn, kỹ thuật viết human-like tránh phát hiện AI, tích hợp với ARS academic-paper modes."
metadata:
  version: "2.3.0"
  last_updated: "2026-05-14"
  status: active
  integrates_with: "academic-paper (ARS v3.1.1)"
  priority: "Tiếng Việt là nguồn chuẩn chính — tiếng Anh chỉ bổ sung"
  vn_sources:
    - "[VN1] Lê Hoàng Anh & Nguyễn Lê Thanh Thy (2024). Ứng dụng phương pháp học máy trong giao dịch chứng khoán theo chỉ báo. Tạp chí KH&CN ĐH Bình Dương, 7(1)."
    - "[VN2] Đào Lê Kiều Oanh & Nguyễn Thị Minh Châu (2024). Dự báo chỉ số chứng khoán bằng học máy: Bằng chứng thực nghiệm từ TTCK Việt Nam. Tạp chí Kinh tế và Dự báo."
    - "[VN3] Nguyễn Thị Thanh Loan và cộng sự (2024). Nghiên cứu ứng dụng phân tích dữ liệu trong quản trị rủi ro tài chính tại các công ty niêm yết TTCK Việt Nam. Tạp chí Kinh tế và Dự báo."
    - "[VN4] ThS. Nguyễn Thị Ngọc Tú & Hoàng Thị Hường (2026). Dấu ấn TTCK Việt Nam năm 2025. Tạp chí Ngân hàng."
  en_sources:
    - "[EN1] Poutré, Chételat & Morales (2024). Deep Unsupervised Anomaly Detection in High-Frequency Markets. J. Finance Data Sci., 10, 100129. [Q1 Elsevier]"
---

# SKILL: Vietnamese Academic Writing (v2.3)
**Ưu tiên học từ paper tiếng Việt | Kết hợp ARS + Anti-AI-Detection**

> **Nguyên tắc:** Paper tiếng Việt là nguồn chuẩn về thuật ngữ và lối hành văn.
> Paper tiếng Anh chỉ dùng để học cách lập luận khoa học — không copy giọng văn EN sang VN.
>
> Nguồn VN đã đọc trực tiếp: 4 bài báo từ Tạp chí KH&CN, Tạp chí Kinh tế và Dự báo, Tạp chí Ngân hàng.

---

## Files trong skill này

| File | Mô tả |
|------|-------|
| `SKILL.md` | Hướng dẫn đầy đủ (file này) |
| `ĐATN-academic-writing.md` | Bộ quy tắc viết học thuật VN — phiên bản đầy đủ có bảng và ví dụ |
| `mega-rule-v2.md` | Nguồn thống nhất kỹ thuật cho đồ án: tech stack, mô hình, evaluation, timeline |
| `beWritten.md` | Bản viết thực tế của đề tài (MỞ ĐẦU + Chương 1 §1.1) — dùng làm chuẩn giọng |
| `references.md` | Danh mục TLTK đầy đủ (25 papers, IEEE format, chia nhóm A–H) |
| `paper_analysis.md` | Phân tích chuyên sâu 5 papers chính: tóm tắt, gap, so sánh với ĐATN |
| `new_papers_to_review.md` | 17 papers mới tìm được — đã verify, chia nhóm, kèm download links |

---

## PHẦN 0 — TÍCH HỢP VỚI ARS academic-paper

### 0.1 Cách dùng skill này cùng ARS

| ARS Pipeline Phase | Skill này hỗ trợ gì |
|---|---|
| Phase 0: CONFIG | Chọn citation format (IEEE cho ĐATN kỹ thuật VN) |
| Phase 4: DRAFTING | Áp dụng văn phong VN chuẩn, anti-AI patterns |
| Phase 6: PEER REVIEW | Checklist kiểm tra AI-isms trước khi submit |
| Phase 7: FORMAT | Format số liệu theo chuẩn VN |

### 0.2 Thứ tự ưu tiên nguồn tham khảo khi viết

```
1. VN papers (VN1–VN4)     ← CHUẨN về thuật ngữ, lối hành văn, cấu trúc câu
2. Mega-rule v2 + ĐATN context  ← Quyết định chọn kỹ thuật, số liệu thực đo
3. EN papers (EN1)          ← Tham khảo cách lập luận khoa học
```

---

## PHẦN I — VĂN PHONG TIẾNG VIỆT HỌC THUẬT

> Toàn bộ phần này được đúc rút trực tiếp từ paper VN thực tế, không phải quy tắc lý thuyết.

### 1.1 Cách mở đầu bài báo / chương (Từ VN1, VN2, VN3, VN4)

**Nguyên tắc:** Câu đầu tiên KHÔNG BAO GIỜ là câu triết lý chung. Phải là phát biểu thực tế, có thể trích dẫn hoặc có số liệu cụ thể.

**Ví dụ tốt — câu mở đầu từ paper VN thực tế:**

*VN1 — Tạp chí KH&CN ĐH Bình Dương:*
> *"Thị trường chứng khoán không chỉ đóng vai trò nguồn vốn cho doanh nghiệp mà còn là kênh đầu tư sinh lợi hấp dẫn cho người dân."*

*VN2 — Tạp chí Kinh tế và Dự báo:*
> *"Trong bối cảnh nền kinh tế toàn cầu ngày càng biến động và phức tạp, việc cung cấp dự báo chỉ số chứng khoán có tính chính xác cao trở thành một yếu tố quan trọng giúp các nhà đầu tư đưa ra quyết định đúng đắn (Chính và Hoàng, 2009)."*
→ Câu đầu có bối cảnh + ngay lập tức dẫn ra hệ quả + citation.

*VN4 — Tạp chí Ngân hàng:*
> *"Thanh khoản thị trường duy trì ở mức cao và ổn định, khối lượng giao dịch bình quân đạt hơn 772 triệu cổ phiếu/ngày tương ứng với giá trị giao dịch bình quân đạt hơn 23.627 tỷ đồng/ngày."*
→ Số liệu thực tế ngay từ câu đầu, không cần dẫn nhập.

### 1.2 Cách viết Gap Statement (Khoảng trống nghiên cứu)

**Pattern chuẩn từ VN1:**
> *"Tại Việt Nam, các nghiên cứu ứng dụng các phương pháp học máy để đề xuất danh mục đầu tư hiệu quả dựa trên chiến lược giao dịch vẫn còn hạn chế. Hầu hết các nghiên cứu này tập trung vào việc dự báo giá cổ phiếu [6], [7], [8]."*

**Cấu trúc 3 bước chuẩn:**
1. Thừa nhận: *"Có nhiều nghiên cứu về X, như: [cite]..."*
2. Chỉ giới hạn: *"Tuy nhiên, trong phạm vi khảo lược chưa tìm thấy..."*
3. Khẳng định gap: *"Vì vậy, bài viết được thực hiện nhằm mục đích lấp đầy khoảng trống nghiên cứu này."*

### 1.3 Cách dẫn vào đề tài / giải pháp

**Từ VN1:**
> *"Do đó, trong nghiên cứu này, chúng tôi một mặt xây dựng chiến lược giao dịch tự động dựa trên chỉ báo để lựa chọn các mã cổ phiếu có tỷ suất sinh lợi cao nhất từ danh mục VN30..."*

### 1.4 Cách định nghĩa khái niệm / thuật toán

**Pattern chuẩn — 3 câu:**
- **Câu 1:** Vị thế chung của X
- **Câu 2:** Định nghĩa kỹ thuật X + viết tắt lần đầu
- **Câu 3+:** Nguyên lý hoạt động / liên hệ ứng dụng

### 1.5 Cách mô tả phương pháp nghiên cứu

Liên kết các bước bằng: *"Tiếp đến là"*, *"Sau khi [X], nghiên cứu thực hiện..."*, *"Từ đó,"*

### 1.6 Cách trình bày kết quả

Pattern: **Dẫn vào bảng/hình → Số liệu cụ thể → So sánh → Nhận xét**

*Từ VN1:*
> *"Dựa trên Hình 2, danh mục đầu tư tối ưu cho chiến lược giao dịch theo chỉ báo SMA gồm các mã cổ phiếu FPT, VIB, BCM, SSI, HPG có tỷ trọng phân bổ vốn lần lượt là 30%, 29%, 21% và 10% cho các mã còn lại. Với tỷ trọng này, tỷ lệ Sharpe đạt cực đại là 0.79, tỷ suất sinh lợi kỳ vọng của danh mục là 19%/năm và rủi ro ước tính 21%."*

### 1.7 Cách viết kết luận có hạn chế

Kết luận bắt đầu bằng dữ liệu cụ thể (bao nhiêu mẫu, giai đoạn nào), không bắt đầu bằng "Nhìn chung..." hay "Tóm lại...".

---

## PHẦN II — TỪ NỐI CHUYỂN ĐOẠN

Chỉ dùng những từ nối đã xuất hiện trong paper VN thực tế.

### 2.1 Nhóm đối lập
`Tuy nhiên,` / `Tuy vậy,` / `Mặc dù vậy,` / `Trong khi đó,` / `Song,`

### 2.2 Nhóm bổ sung
`Bên cạnh đó,` / `Ngoài ra,` / `Hơn nữa,` / `Đặc biệt là,` / `Cùng với đó,`

### 2.3 Nhóm hệ quả
`Do đó,` / `Vì vậy,` / `Từ đó,` / `Trên cơ sở đó,` / `Điều này cho thấy` / `Điều này phản ánh`

### 2.4 Nhóm dẫn vào đề tài
`Xuất phát từ thực tiễn đó,` / `Nhằm lấp đầy khoảng trống đó,` / `Nhằm giải quyết vấn đề trên,`

### 2.5 Nhóm kết thúc
`Kết quả cho thấy` / `Có thể thấy,` / `Như vậy,` / `Tóm lại,`

### 2.6 Nhóm liên kết bước nghiên cứu
`Tiếp đến là` / `Sau khi [X], nghiên cứu thực hiện...` / `Cụ thể,` / `Trong đó,` / `Theo đó,`

---

## PHẦN III — ANTI-AI-DETECTION

> AI detectors đo Perplexity (độ khó đoán từ ngữ) và Burstiness (biến thiên độ dài câu).
> Text AI có perplexity thấp, burstiness thấp. Human writing ngược lại.

### 3.1 Bảng AI-isms tiếng Việt

| # | Lỗi AI-gen | Dấu hiệu | Cách sửa |
|---|-----------|---------|---------| 
| 1 | **"Trong bối cảnh..."** mở đầu | Câu mở chung | Thay bằng câu có số liệu cụ thể |
| 2 | **"Có thể thấy rằng..."** | Hedge phrase | Viết thẳng kết luận |
| 3 | **"Đây là một vấn đề quan trọng"** | Nhận định chung | Bỏ, viết thẳng vào nội dung |
| 4 | **Liệt kê "Thứ nhất... Thứ hai..."** | Cứng nhắc | Viết văn xuôi |
| 5 | **3 câu liên tiếp cùng cấu trúc** | "Đối với X... Y... Z..." | Gộp thành 1–2 câu |
| 6 | **Dấu "—" giải thích** | "pipeline — tức là..." | Viết: "pipeline (chuỗi xử lý)" |
| 7 | **Liệt kê tên công cụ dài** | "Kafka, PySpark, Delta Lake..." | Nhóm theo chức năng |
| 8 | **Uniform paragraph** | Mọi đoạn đều 4-5 câu | Xen đoạn 2-3 câu với 6-7 câu |
| 9 | **Dùng ":" trước giải thích dài** | "đề tài tiếp cận theo hướng: A, B, C" | Viết văn xuôi bình thường |
| 10 | **Cấu trúc "Về A... Về B... Về C..."** | Liệt kê song song đều đặn | Kết hợp văn xuôi + đổi cấu trúc câu |

### 3.2 AI tell-words — cần hạn chế hoặc thêm số liệu đi kèm

- **"quan trọng"** — thay bằng mô tả cụ thể hơn
- **"toàn diện"** — thay bằng "bao gồm [X, Y, Z]"
- **"đáng kể"** — thay bằng số liệu cụ thể
- **"hiệu quả"** — chỉ dùng khi có số liệu đi kèm

### 3.3 Kỹ thuật tăng Burstiness

Pattern nhịp câu từ VN4:
```
[Câu dài 35-45 từ — số liệu, context]
[Câu trung bình 25-35 từ — giải thích]
[Câu ngắn 10-15 từ — kết luận nhanh]
[Câu dài 30-40 từ — dẫn chứng]
[Câu ngắn 8-12 từ — kết đoạn]
```

### 3.4 Kỹ thuật tăng Perplexity

1. **Dùng số liệu thực đo** — "~78.000 ticks/phiên (thực đo 14/05/2026)"
2. **Trích dẫn tên tác giả VN cụ thể** trong câu
3. **Dùng cụm từ VN đặc trưng học thuật**: "trong phạm vi khảo lược", "bằng chứng thực nghiệm"
4. **Câu nhận xét tác giả**: "Phát hiện này trái ngược với kết quả của..."

### 3.5 Thứ tự ưu tiên khi sửa (structural rewrite first)

1. Đổi cấu trúc câu (passive ↔ active, đổi thứ tự mệnh đề)
2. Gộp / tách câu để thay đổi nhịp
3. Thêm số liệu thực đo và chi tiết đặc thù
4. Thêm citation tên tác giả VN cụ thể
5. Cuối cùng mới: thay từ ngữ

### 3.6 Checklist trước khi nộp

```
[ ] Câu đầu tiên có thông tin cụ thể (số liệu / tên nghiên cứu / sự kiện)?
[ ] Không có AI tell-words không có dữ liệu đi kèm?
[ ] Không có 3 câu liên tiếp bắt đầu giống nhau?
[ ] Mọi số liệu đều có [citation] ngay sau?
[ ] Không có câu mở vô nghĩa: "Trong phần này chúng tôi sẽ..."?
[ ] Độ dài câu có biến thiên: câu ngắn < 15 từ xen câu dài > 35 từ?
[ ] Đoạn có 4–6 câu (không phải mọi đoạn đều y hệt nhau)?
[ ] Có ít nhất 1 chi tiết đặc thù đề tài (số liệu thực đo / tên mã VN30)?
[ ] Đọc to: nghe tự nhiên không? Có chỗ nào nghe "máy" không?

--- Cấu trúc chương ---
[ ] Chương có đoạn dẫn vào trước heading cấp 2 đầu tiên?
[ ] Không bắt đầu mục bằng định nghĩa hoặc liệt kê ngay?
[ ] Không có cấu trúc "Về A... Về B... Về C..."?
[ ] Câu kết mục neo điểm quan trọng, không phải tóm tắt lại?
```

---

## PHẦN IV — TỪ VỰNG CHUYÊN NGÀNH

> **Nguyên tắc tra cứu (v2.3):** Mỗi thuật ngữ được kiểm tra thực tế qua nguồn học thuật VN.
> Nếu có bản dịch chuẩn → dùng bản dịch + kèm gốc lần đầu.
> Nếu **không có** bản dịch đủ chuẩn → **giữ nguyên thuật ngữ gốc** + định nghĩa tiếng Việt 1 lần duy nhất khi xuất hiện lần đầu trong văn bản.

---

### 4.1 Nhóm A — CÓ bản dịch tiếng Việt chuẩn (tìm thấy trong nguồn học thuật VN)

| Tiếng Anh | Tiếng Việt chuẩn | Lần đầu viết | Nguồn xác thực |
|-----------|-----------------|-------------|----------------|
| Stock market / Securities market | thị trường chứng khoán | thị trường chứng khoán | VN1–VN4 |
| HOSE | Sở Giao dịch Chứng khoán TP. Hồ Chí Minh | Sở Giao dịch Chứng khoán TP. Hồ Chí Minh (HOSE) | VN3 |
| Machine learning | học máy | học máy | VN1–VN3 |
| Deep learning | học sâu | học sâu | VN2 |
| Supervised learning | học có giám sát | học có giám sát | Tạp chí NH 2021 |
| Unsupervised learning | học không giám sát | học không giám sát (unsupervised learning) | Tạp chí NH 2021 |
| Neural network | mạng nơ-ron (nhân tạo) | mạng nơ-ron nhân tạo | VN2, VN3 |
| Training set | tập huấn luyện | tập huấn luyện | VN3, Tạp chí NH 2021 |
| Test set | tập kiểm tra | tập kiểm tra | VN3, Tạp chí NH 2021 |
| Overfitting | quá khớp | quá khớp (overfitting) | VN3 |
| Anomaly detection | phát hiện bất thường | phát hiện bất thường | Tạp chí NH 2021, HUIT |
| Anomaly / Outlier | điểm bất thường / ngoại lệ | điểm bất thường | Tạp chí NH 2021 |
| Sliding window | cửa sổ trượt | cửa sổ trượt | kỹ thuật CNTT VN phổ biến |
| Order book | sổ lệnh | sổ lệnh (order book) | VietstockPedia, vietnambiz.vn |
| Watchlist | danh sách theo dõi | danh sách theo dõi (watchlist) | happy.live, investing.vn |
| Buy pressure / Sell pressure | áp lực mua / áp lực bán | áp lực mua / áp lực bán | tài chính VN phổ biến |
| Market capitalization | vốn hóa thị trường | vốn hóa thị trường (vốn hóa) | VN4 |
| Confusion matrix | ma trận nhầm lẫn | ma trận nhầm lẫn | VN3 |
| ROC curve | đường cong ROC | đường cong ROC | Tạp chí NH 2021 |
| Precision / Recall | độ chính xác / độ nhạy | độ chính xác (Precision) / độ nhạy (Recall) | Tạp chí NH 2021 |
| F1-score | F1-score | F1-score | Tạp chí NH 2021 (giữ nguyên EN) |
| Data stream | luồng dữ liệu | luồng dữ liệu | từ điển kỹ thuật VN, datalinks.vn |
| Alert | cảnh báo | cảnh báo | VN phổ biến |
| Individual investor | nhà đầu tư cá nhân | nhà đầu tư cá nhân | VN1–VN4 |
| Institutional investor | nhà đầu tư tổ chức | nhà đầu tư tổ chức | VN tài chính |
| Trading volume | khối lượng giao dịch | khối lượng giao dịch | VN4 |
| Listed company | công ty niêm yết | công ty niêm yết | VN3 |
| Big Data | dữ liệu lớn | dữ liệu lớn (Big Data) | VN kỹ thuật |
| Feature | đặc trưng | đặc trưng | VN học máy phổ biến |
| Feature engineering | xây dựng đặc trưng | xây dựng đặc trưng (feature engineering) | Viblo, Studocu VN |
| Rolling statistics | thống kê cửa sổ trượt | thống kê cửa sổ trượt | VN kỹ thuật |
| Medallion architecture | kiến trúc Medallion | kiến trúc Medallion | Studocu VN (tên riêng, không dịch nội dung) |

---

### 4.2 Nhóm B — KHÔNG có bản dịch VN học thuật → Giữ nguyên thuật ngữ gốc + định nghĩa 1 lần

Các thuật ngữ sau **không tìm được bản dịch chuẩn trong nguồn học thuật VN** (tạp chí, sách giáo khoa, văn bản chính thức). Khi viết: **giữ nguyên tên gốc tiếng Anh**, định nghĩa bằng tiếng Việt đúng một lần ở lần xuất hiện đầu tiên, sau đó dùng tên gốc xuyên suốt.

| Thuật ngữ gốc | Định nghĩa tiếng Việt (dùng 1 lần lần đầu) | Lý do không dịch |
|---|---|---|
| **Isolation Forest** | thuật toán phát hiện bất thường dựa trên cơ chế cô lập điểm dữ liệu qua cây quyết định ngẫu nhiên | Tên thuật toán — không dịch; "rừng cô lập" dù xuất hiện trong 1 bài blog học thuật vẫn chưa đủ chuẩn hóa; giữ nguyên để tránh nhầm với Random Forest |
| **Intraday** | các biến động giá, khối lượng và tín hiệu thị trường xảy ra trong phạm vi một phiên giao dịch duy nhất — bắt đầu khi mở cửa và kết thúc khi đóng cửa phiên, không kéo sang phiên tiếp theo; dữ liệu intraday ghi lại trạng thái thị trường tại từng thời điểm trong phiên [SuperMoney; Vietstock] | Dịch "giao dịch trong phiên" hoặc "giao dịch trong ngày" mất tính chính xác kỹ thuật; intraday xác định cụ thể giới hạn thời gian trong một phiên, không phải chỉ cách thức giao dịch |
| **AUROC** | diện tích dưới đường cong ROC — chỉ số đánh giá khả năng phân biệt của mô hình phân loại nhị phân | Chỉ số đánh giá chuẩn quốc tế, viết tắt kỹ thuật cố định; không dịch để tránh nhầm với các chỉ số khác |
| **OFI** (Order Flow Imbalance) | tổng lũy tích biến động khối lượng tại mức giá tốt nhất qua từng sự kiện trong sổ lệnh, tính theo công thức OFI = ΣΔV_bid − ΣΔV_ask; dương khi áp lực mua chiếm ưu thế, âm khi áp lực bán chiếm ưu thế; Cont, Kukanov & Stoikov (2014) chứng minh OFI giải thích trung bình 65% biến động giá ngắn hạn trên NYSE | Không có thuật ngữ VN học thuật chuẩn hóa; "mất cân bằng dòng lệnh" chưa xuất hiện trong nguồn xác thực; *tạm dịch*: "chỉ số mất cân bằng dòng lệnh" — chỉ dùng khi giải thích, không dùng thay OFI trong văn bản |
| **VWAP** (Volume Weighted Average Price) | giá bình quân gia quyền theo khối lượng giao dịch tích lũy trong phiên, tính bằng Σ(giá × khối lượng) / Σ khối lượng; reset về đầu phiên mỗi ngày; dùng làm chuẩn tham chiếu đánh giá chất lượng khớp lệnh của nhà đầu tư tổ chức [CFI; TradingView] | Không có trong paper học thuật VN; blog tài chính dùng không nhất quán; *tạm dịch*: "giá bình quân gia quyền khối lượng" |
| **Concept drift** | hiện tượng phân phối xác suất kết hợp P(X, y) thay đổi theo thời gian — Pt(X,y) ≠ Pt+1(X,y) — khiến mô hình học máy huấn luyện trên dữ liệu cũ giảm độ chính xác trên dữ liệu mới; đặc biệt nghiêm trọng trong dữ liệu tài chính do điều kiện thị trường biến động liên tục [Gama et al.; Springer 2020] | Viblo giữ nguyên "concept drift"; "trôi dạt khái niệm" chưa chuẩn hóa học thuật VN; *tạm dịch*: "hiện tượng trôi dạt phân phối dữ liệu" |
| **Pipeline** (data pipeline) | chuỗi các bước xử lý dữ liệu tự động từ thu thập đến lưu trữ | Bản dịch "đường ống dữ liệu" có trong blog kỹ thuật nhưng không từ nguồn học thuật; "pipeline" dùng phổ biến hơn trong kỹ thuật VN |
| **Tick data** | bản ghi đầy đủ từng giao dịch khớp lệnh theo thứ tự thời gian thực, bao gồm ba trường tối thiểu: giá khớp, khối lượng khớp và dấu thời gian chính xác của từng giao dịch; mỗi thay đổi trạng thái thị trường tạo ra một bản ghi mới [appreciatewealth.com; market microstructure] | "Dữ liệu tick" phổ biến nhưng không từ paper học thuật VN; *tạm dịch*: "dữ liệu giao dịch tức thời" |
| **Contamination** (IF parameter) | tỷ lệ điểm bất thường ước tính trong tập dữ liệu, dùng làm tham số của Isolation Forest | Hoàn toàn không có bản dịch VN trong nguồn nào |
| **Ground truth label** | nhãn thực tế xác định một điểm dữ liệu là bất thường hay bình thường | "Nhãn xác thực" / "nhãn thực tế" xuất hiện trong blog kỹ thuật nhưng không trong paper học thuật VN |
| **Recall@K** | tỷ lệ sự kiện đã biết nằm trong top-K điểm bất thường nhất theo mô hình | Không có bản dịch VN nào |
| **Mann-Whitney U test** | kiểm định thống kê phi tham số kiểm tra xem hai phân phối có khác nhau không | Tên kiểm định được giữ nguyên trong tất cả nguồn học thuật VN (Tạp chí y học, SPSS) |
| **Anomaly score** | điểm số đánh giá mức độ bất thường của một điểm dữ liệu theo mô hình | Blog kỹ thuật VN dùng "điểm số bất thường" nhưng không từ paper học thuật |
| **Structured Streaming** (PySpark) | cơ chế xử lý luồng dữ liệu liên tục của PySpark | Tên riêng kỹ thuật, không dịch |
| **Bronze / Silver / Gold layer** | ba lớp lưu trữ trong kiến trúc Medallion: dữ liệu thô (Bronze), đã làm sạch (Silver), đặc trưng đã tính (Gold) | Tên riêng kiến trúc Delta Lake, không dịch |
| **Near real-time** | xử lý và cập nhật dữ liệu với độ trễ nhỏ (chu kỳ 60 giây trong đề tài này) | "Gần thời gian thực" phổ biến nhưng chỉ trong blog, không trong paper học thuật VN |
| **Polling** | cơ chế thu thập dữ liệu định kỳ theo chu kỳ cố định | Không có bản dịch VN học thuật |

---

### 4.3 Quy tắc áp dụng — BẮT BUỘC

**Nhóm A — có bản dịch VN:**
```
✅ Lần đầu: "học không giám sát (unsupervised learning)"
✅ Sau đó: "học không giám sát" hoặc viết tắt nếu có
❌ Sai: chỉ viết "unsupervised learning" mà không có tiếng Việt
```

**Nhóm B — không có bản dịch chuẩn:**
```
✅ Lần đầu: "Isolation Forest (thuật toán phát hiện bất thường dựa trên cơ chế cô lập điểm dữ liệu)"
✅ Sau đó: "Isolation Forest" hoặc "IF" xuyên suốt — không dùng "rừng cô lập"
✅ Lần đầu: "intraday (giao dịch diễn ra trong khoảng thời gian một phiên giao dịch duy nhất)"
✅ Sau đó: "intraday" xuyên suốt — không dùng "giao dịch trong phiên"
✅ Lần đầu: "AUROC (diện tích dưới đường cong ROC — chỉ số đánh giá khả năng phân biệt của mô hình)"
✅ Sau đó: "AUROC" xuyên suốt — không dịch
✅ Lần đầu: "OFI (chỉ số đo lường chênh lệch giữa áp lực mua và áp lực bán tại mức giá tốt nhất)"
✅ Sau đó: "OFI" xuyên suốt
✅ Lần đầu: "concept drift (hiện tượng phân phối dữ liệu thay đổi theo thời gian)"
✅ Sau đó: "concept drift" xuyên suốt
❌ Sai: dịch "Isolation Forest" thành "rừng cô lập"
❌ Sai: dịch "intraday" thành "trong phiên" / "giao dịch trong phiên" (mất nghĩa kỹ thuật)
❌ Sai: dịch "AUROC" thành "diện tích dưới đường cong ROC" trong câu (gây rối khi đọc kết quả số)
```

**Tên riêng / framework — không dịch, không giải thích:**
```
✅ Kafka, PySpark, Delta Lake, MLflow, FastAPI, Streamlit, DuckDB, Dask, Airflow
✅ Medallion architecture (chỉ giải thích Bronze/Silver/Gold một lần)
✅ HOSE (giải thích đầy đủ 1 lần: "Sở Giao dịch Chứng khoán TP. Hồ Chí Minh (HOSE)")
```

---

### 4.4 Cách viết số và đơn vị

| Trường hợp | Cách viết đúng |
|-----------|---------------|
| Số tiền VND | "23.627 tỷ đồng/ngày" — dấu chấm ngăn hàng nghìn |
| Phần trăm | "40,8%" — dấu phẩy thập phân |
| Số liệu thực đo ĐATN | "~78.000 ticks/phiên (thực đo 14/05/2026)" |
| Số lượng lớn | "gần 11,6 triệu tài khoản" |
| Năm / giai đoạn | "năm 2025", "giai đoạn 2020–2025" (dùng dấu gạch ngang ngắn) |

---

## PHẦN V — FORMAT TRÍCH DẪN (IEEE style)

### 5.1 Inline citation

```
...tổng số tài khoản lên hơn 7,4 triệu tài khoản [1].
...các nghiên cứu [2], [3], [4]...
```

### 5.2 Reference list chuẩn

**Bài báo tạp chí VN:**
```
[1] Lê Hoàng Anh và Nguyễn Lê Thanh Thy, "Ứng dụng phương pháp học máy trong giao 
    dịch chứng khoán theo chỉ báo bằng ngôn ngữ lập trình Python," Tạp chí Khoa học 
    và Công nghệ Trường Đại học Bình Dương, tập 7, số 1, 2024,
    doi: 10.56097/binhduonguniversityjournalofscienceandtechnology.v7i1.212.
```

**Bài báo Q1 tiếng Anh:**
```
[2] C. Poutré, D. Chételat, and M. Morales, "Deep unsupervised anomaly detection in 
    high-frequency markets," J. Finance Data Sci., vol. 10, p. 100129, 2024, 
    doi: 10.1016/j.jfds.2024.100129.
```

**Bài báo hội nghị:**
```
[3] F. T. Liu, K. M. Ting, and Z.-H. Zhou, "Isolation forest," in Proc. 8th IEEE Int. 
    Conf. Data Mining (ICDM), 2008, pp. 413–422, doi: 10.1109/ICDM.2008.17.
```

### 5.3 Nguyên tắc không vi phạm

1. Mọi số liệu cụ thể đều cần [số] — không ngoại lệ
2. Số liệu tự đo không cần citation, nhưng phải ghi "(thực đo ngày...)"
3. Không cite Wikipedia, blog cá nhân, bài không tác giả
4. Tên tác giả VN: giữ nguyên tiếng Việt trong reference list

---

## PHẦN VI — QUY TẮC RIÊNG ĐATN

*(Cho đề tài "Xây dựng nền tảng quản lý danh sách theo dõi và cảnh báo giao dịch bất thường trong phiên cho cổ phiếu VN30")*

### 6.1 Phân biệt "bất thường thống kê" và "thao túng"

**Đúng:** giao dịch bất thường = lệch chuẩn thống kê so với lịch sử cùng mã

Câu mẫu:
> *"Hệ thống phát hiện các khung thời gian có hành vi dòng tiền lệch chuẩn bất thường về mặt thống kê so với lịch sử của chính mã cổ phiếu đó, không đưa ra bất kỳ kết luận pháp lý nào về hành vi giao dịch."*

### 6.2 Cách gọi tên nhất quán

| ❌ Sai | ✅ Đúng |
|--------|---------| 
| "app" | "ứng dụng web" / "giao diện người dùng" |
| "real-time" | "thời gian thực" / "gần thời gian thực (polling 60 giây)" |
| "dự báo giá" | **TUYỆT ĐỐI KHÔNG DÙNG** |
| "big data" | "dữ liệu lớn" hoặc "Big Data" |

### 6.3 Viết về kết quả mô hình

**Đúng:**
> *"Mô hình Isolation Forest đạt AUROC = 0,72 trên tập sự kiện đã biết (n = 27 ngày), với kiểm định Mann-Whitney U cho p < 0,05, cho thấy điểm bất thường trong ngày sự kiện cao hơn ngày bình thường một cách có ý nghĩa thống kê."*

**Sai:** *"Mô hình đạt kết quả tốt"* — không có chỉ số.

### 6.4 Cách viết về data volume

**Đúng:**
> *"Dữ liệu thực đo ngày 14/05/2026 ghi nhận khoảng 78.000 ticks trong phiên trên 30 mã VN30, ước tính tương đương 19 đến 25 triệu bản ghi mỗi năm."*

---

## PHẦN VII — CẤU TRÚC CHƯƠNG VÀ DẪN CHUYỂN

### 7.1 Đoạn dẫn vào chương — BẮT BUỘC

Mỗi chương phải có **1 đoạn mở chương** (3–5 câu) đặt trước heading cấp 2 đầu tiên. Đoạn này đặt bối cảnh, cho thấy sợi chỉ logic dẫn từ chương trước — KHÔNG phải tóm tắt mục lục.

**Ví dụ đúng — từ `beWritten.md` (Chương 1):**
> *"Mỗi lệnh được khớp trong phiên giao dịch không chỉ phản ánh một giao dịch đơn lẻ mà còn tiết lộ trạng thái tức thời của quan hệ cung cầu tại mức giá đó. Cont, Kukanov và Stoikov (2014) chứng minh trên dữ liệu NYSE rằng chỉ số mất cân bằng dòng lệnh (OFI) giải thích trung bình 65% biến động giá ngắn hạn..."*

**Pattern 3 kiểu đoạn dẫn chương:**

| Kiểu | Khi dùng | Cấu trúc |
|------|----------|----------|
| Số liệu → vấn đề | Chương 1 | Câu số liệu cụ thể → Câu chỉ khoảng trống → Câu liên hệ chương |
| Kế thừa → mở rộng | Chương 2, 3 | Câu nhắc kết quả chương trước → "Để [X], cần..." → Câu phạm vi chương |
| Kết quả → đánh giá | Chương 4 | Câu mô tả hệ thống → "Chương này trình bày kết quả..." → Câu số liệu chính |

### 7.2 Câu dẫn và câu chuyển trong từng mục

**Câu dẫn mở mục — có câu thiết lập ngữ cảnh trước khi vào định nghĩa:**

*Sai:*
> *"## 2.4 Isolation Forest*
> *Isolation Forest là thuật toán phát hiện bất thường. Các ưu điểm bao gồm..."*

*Đúng:*
> *"## 2.4 Thuật toán Isolation Forest*
> *Trong khi các phương pháp thống kê truyền thống như LOF hay OC-SVM xây dựng profile của vùng bình thường trước khi phát hiện bất thường, Isolation Forest tiếp cận ngược lại: thay vì mô hình hóa dữ liệu bình thường, thuật toán trực tiếp cô lập các điểm bất thường dựa trên nguyên lý chúng 'ít và khác biệt'. Cách tiếp cận này giúp giảm đáng kể độ phức tạp tính toán và phù hợp với dữ liệu lớn."*

**Câu kết mục — neo điểm hoặc mở tự nhiên:**

*Sai:*
> *"Như vậy, phần này đã trình bày ba phương pháp chính. Phần tiếp theo sẽ..."*

*Đúng:*
> *"Song, để Isolation Forest phát huy hiệu quả trên dữ liệu tài chính biến đổi liên tục, cần giải quyết thêm vấn đề concept drift — nội dung được phân tích trong phần thiết kế mô hình."*

---

## PHẦN VIII — TÍCH HỢP VỚI ARS PIPELINE

### 8.1 Prompt mẫu cho ARS `revision` mode

```
"Revise this Vietnamese academic draft section:
1. Check câu mở đoạn: phải là phát biểu thực tế, không phải triết lý chung
2. Remove hedging: 'Có thể thấy rằng', 'Đây là một vấn đề quan trọng'
3. Vary sentence length: xen câu ngắn < 15 từ với câu dài > 35 từ
4. Replace 'và cộng sự' listing with prose flow using VN connectors
5. Add numbers from mega-rule: tick count, AUROC targets, known-event n=27
Apply patterns from Vietnamese academic papers (Tạp chí Kinh tế và Dự báo style).
[DRAFT TEXT]"
```

### 8.2 ARS Anti-Patterns + VN Academic Style

| ARS Anti-Pattern | VN Style Fix |
|---|---|
| "delve into" / "explore" | "phân tích" / "xem xét" / "nghiên cứu" |
| "it is worth noting" | Xóa. Viết thẳng điều muốn nói. |
| "In this section..." | Bắt đầu bằng nội dung trực tiếp |
| Uniform paragraphs | Xen đoạn 2-3 câu với đoạn 5-7 câu |
| Inventory listing | Nhóm theo chức năng: "công cụ xử lý luồng (Kafka, PySpark)" |

---

## NGUỒN ĐÃ ĐỌC

### Tiếng Việt (PRIMARY)

- **[VN1]** Lê Hoàng Anh & Nguyễn Lê Thanh Thy (2024). *Tạp chí KH&CN ĐH Bình Dương*, 7(1). — đọc full text
- **[VN2]** Đào Lê Kiều Oanh & Nguyễn Thị Minh Châu (2024). *Tạp chí Kinh tế và Dự báo*. — đọc full text
- **[VN3]** Nguyễn Thị Thanh Loan và cộng sự (2024). *Tạp chí Kinh tế và Dự báo*. — đọc full text
- **[VN4]** ThS. Nguyễn Thị Ngọc Tú & Hoàng Thị Hường (2026). *Tạp chí Ngân hàng*. — đọc full text

### Tiếng Anh (SECONDARY)

- **[EN1]** Poutré, C., Chételat, D. & Morales, M. (2024). *J. Finance Data Sci.*, 10, 100129. — đọc full text

---

*Phiên bản 2.2 | Tạo: 2026-05-14 | VN papers là nguồn chuẩn chính*
*Files hỗ trợ: ĐATN-academic-writing.md (quy tắc đầy đủ) | mega-rule-v2.md (context kỹ thuật) | beWritten.md (chuẩn giọng) | references.md | paper_analysis.md | new_papers_to_review.md*
