# Phân Tích Học Thuật — 5 Papers cho Chương 1 ĐATN

> **Đề tài ĐATN:** "Xây dựng nền tảng quản lý danh sách theo dõi và cảnh báo giao dịch bất thường trong phiên cho cổ phiếu VN30"
> **Stack:** Kafka + PySpark + Delta Lake + Dask + MLflow + FastAPI + Streamlit
> **Model:** Isolation Forest per-stock, sliding window retrain, tick data (~78.000 ticks/phiên, polling 60s)
> **Features:** OFI, VWAP deviation, volume rolling stats
> **Evaluation:** Known-Event Validation Framework (không có ground truth label)

---

## Paper 1 — Poutré et al. 2023

### 1. Tóm tắt (3–4 câu)

Bài báo đề xuất một framework phát hiện bất thường không giám sát kết hợp (hybrid unsupervised) dành riêng cho dữ liệu Limit Order Book (LOB) tần suất cao. Phương pháp gồm hai bước: (1) một Transformer Autoencoder dạng bottleneck học biểu diễn chuỗi thời gian của LOB; (2) một OC-SVM học hàm dissimilarity trên không gian biểu diễn đó để phân tách hành vi bình thường và bất thường. Dữ liệu là LOB Level 1 của 5 cổ phiếu NASDAQ (AAPL, AMZN, GOOG, INTC, MSFT) trong một ngày giao dịch (21/6/2012) với 3 loại thao túng tổng hợp: pump-and-dump, layering, quote stuffing. Framework đạt AUROC=0.900, AUPRC=0.847, F4=0.935 (Recall=0.965), vượt trội so với tất cả baseline không giám sát.

### 2. Hạn chế / Gap (từ chính tác giả)

- **Concept drift chưa được giải quyết:** *"market data drift is an important aspect to consider when deploying any data–based model, because the past learned notion of normality might slowly depart from future normal market behaviors. It is primordial to know when to retrain anomaly detection frameworks."* (Section 6)
- **Chỉ dùng 1 ngày giao dịch** (June 21, 2012) — single-day snapshot, không kiểm chứng cross-session stability.
- **Nhãn gian lận là tổng hợp** (synthetic), không phải nhãn thật từ điều tra thực tế.
- **Chỉ áp dụng trên thị trường Mỹ (NASDAQ)**, không có thực nghiệm trên thị trường mới nổi.
- Tác giả thừa nhận **semi-supervised learning** (dùng fraud examples đã biết để boost detection) là hướng mở tiếp theo, chưa được khám phá.
- Framework nặng về tính toán (Transformer + OC-SVM), chưa có thiết kế cho **real-time streaming**.

### 3. Citation chuẩn IEEE

```
[X] C. Poutré, D. Chételat, and M. Morales, "Deep Unsupervised Anomaly Detection in
    High-Frequency Markets," CISMF Research Paper Series, Centre d'intelligence en
    surveillance des marchés financiers, Université de Montréal, Jul. 2023.
```
*(Lưu ý: File đặt tên "poutre2024" nhưng bài gốc ghi "July 2023" — dùng năm 2023 trong citation)*

### 4. Quote đáng dùng trong gap statement

> *"market data drift is an important aspect to consider when deploying any data–based model, because the past learned notion of normality might slowly depart from future normal market behaviors."*
> — Poutré et al. (2023), Section 6

> *"the current literature on machine learning in financial market manipulation lacks generality, as only very limited sets of features and/or fraud types are studied simultaneously."*
> — Poutré et al. (2023), Section 1

### 5. So sánh với ĐATN

| Tiêu chí | Poutré et al. 2023 | ĐATN |
|---|---|---|
| **Thị trường** | NASDAQ (Mỹ) | HOSE VN30 (Việt Nam) |
| **Dữ liệu** | LOB L1 tick 1 ngày (5 stocks) | Tick data ~78.000 ticks/phiên, 30 stocks, streaming |
| **Phương pháp** | Transformer-AE + OC-SVM | Isolation Forest per-stock |
| **Mục tiêu** | Phát hiện thao túng (pump-dump, layering, quote stuffing) có nhãn tổng hợp | Cảnh báo giao dịch bất thường không nhãn trong phiên |
| **Đánh giá** | Precision/Recall trên synthetic fraud | Known-Event Validation Framework |
| **Kiến trúc** | Offline research, không real-time | Kafka + PySpark streaming, near real-time |
| **Tái huấn luyện** | Không đề cập sliding window | Sliding window retrain theo phiên |

---

## Paper 2 — Núñez et al. 2024

### 1. Tóm tắt (3–4 câu)

Nghiên cứu đề xuất framework phát hiện thao túng thị trường không giám sát dựa trên k-Partitioned Isolation Forest với cơ chế voting ensemble. Tập dữ liệu gồm 8 cổ phiếu Mỹ có hồ sơ thao túng được SEC xác nhận năm 2003, với 55 khối thao túng đã gán nhãn thủ công. Phương pháp chia đặc trưng thành k tập con ngẫu nhiên, mỗi tập huấn luyện một mô hình IF độc lập, sau đó voting ensemble để phân loại. Kết quả tốt nhất đạt recall 89% (phát hiện 49/55 khối thao túng) với k=2, threshold=1, vượt các phương pháp trước không dùng ensemble.

### 2. Hạn chế / Gap (từ chính tác giả)

- **Không xác định được tổng số khối thao túng thực sự:** *"a crucial point of consideration is the inherent uncertainty surrounding the exact number of manipulated blocks within the dataset. This ambiguity introduces a potential for false positives."*
- **IF được thiết kế cho dữ liệu tĩnh (static), không phải chuỗi thời gian:** *"This algorithm, primarily designed for static datasets, necessitated an adaptation to handle time series data effectively."*
- **Precision rất thấp** (~3–5.5%) — nhiều false positive, chi phí kiểm tra cao.
- **Chỉ thử nghiệm k ≤ 3** — không kiểm chứng hiệu quả với k lớn hơn.
- **Dữ liệu cũ từ 2003**, daily/hourly — không phản ánh microstructure thị trường hiện đại.
- **Thiếu kiến trúc real-time**: chỉ là quy trình batch offline.
- Future work: *"assess the effectiveness of the voting ensemble strategy in conjunction with an anomaly detection approach that focuses on the reconstruction error of time series."*

### 3. Citation chuẩn IEEE

```
[X] H. Núñez Delafuente, C. A. Astudillo, and D. Díaz, "Ensemble Approach Using
    k-Partitioned Isolation Forests for the Detection of Stock Market Manipulation,"
    Mathematics, vol. 12, no. 9, p. 1336, 2024, doi: 10.3390/math12091336.
```

### 4. Quote đáng dùng trong gap statement

> *"This algorithm, primarily designed for static datasets, necessitated an adaptation to handle time series data effectively. By converting the dynamic nature of time series into a static dataset enriched with statistical features across multiple columns, we were able to imbue the Isolation Forest algorithm with the ability to comprehend historical patterns within various transactions."*
> — Núñez et al. (2024), Section 4

> *"the inherent uncertainty surrounding the exact number of manipulated blocks... highlights a limitation in our validation process, where the benchmark for model accuracy is constrained by the completeness and reliability of the manipulation cases available for comparison."*
> — Núñez et al. (2024), Section 4

### 5. So sánh với ĐATN

| Tiêu chí | Núñez et al. 2024 | ĐATN |
|---|---|---|
| **Thị trường** | NYSE/NASDAQ Mỹ (2003) | HOSE VN30 (Việt Nam, hiện tại) |
| **Dữ liệu** | Daily/hourly OHLCV, 8 stocks | Tick data streaming, 30 stocks, ~78k ticks/phiên |
| **Phương pháp** | k-Partitioned IF ensemble + voting | IF per-stock, single model per ticker |
| **Features** | 4 raw + 27 engineered (moving avg, z-scores) | OFI, VWAP deviation, volume rolling stats |
| **Nhãn** | 55 labeled manipulation blocks (SEC lawsuits) | Không có nhãn — Known-Event Validation |
| **Đánh giá** | Precision/Recall vs labeled set | Known-Event Framework (sự kiện lịch sử VN) |
| **Kiến trúc** | Batch offline | Real-time streaming (Kafka + PySpark) |
| **Tái huấn luyện** | Không đề cập | Sliding window retrain per phiên (MLflow) |

---

## Paper 3 — Yang & Liu 2025

### 1. Tóm tắt (3–4 câu)

Nghiên cứu đề xuất framework hybrid LSTM Autoencoder + GAN + One-Class SVM cho phát hiện bất thường không giám sát trên dữ liệu tài chính ngày (daily). LSTM AE học temporal dependencies và tạo latent representation, OC-SVM phân tách vùng bình thường trong không gian latent, GAN học phân phối dữ liệu bình thường và phát hiện anomaly qua reconstruction error. Thực nghiệm trên 38 cổ phiếu US (6 loại: indices, mega-cap, small-cap, high/low volatility, penny stocks) qua nhiều regime kinh tế (GFC 2008, COVID-19). Kết quả: Precision=0.70, Recall=0.80, F4=0.78, vượt GARCH, Z-Score, OC-SVM raw, LSTM riêng lẻ, GAN riêng lẻ.

### 2. Hạn chế / Gap (từ chính tác giả)

- **Phụ thuộc dữ liệu ngày (daily), không thể phát hiện bất thường intraday:** *"The reliance on daily-level data, though pragmatic and reproducible, constrains the model's ability to capture microstructure-level patterns such as spoofing or intraday manipulation."*
- **Tự thừa nhận dữ liệu tick/L1 tốt hơn nhưng bị giới hạn tiếp cận:** *"High-quality anomaly detection often requires fine-grained data such as Level 1 order-book or tick-level feeds... due to cost and access restrictions, our study uses daily-level return and volume data."*
- **Không có ground truth labels**: dùng artificial anomaly injection để đánh giá.
- **GAN overfit trên tập nhỏ** (penny stocks): *"GANs may overfit small datasets... we observed that overfitting primarily occurred when modeling penny stock data."*
- **Chưa mở rộng sang minute- hay tick-level**: *"We plan to extend our framework to operate on minute- or tick-level data."*
- **Không có kiến trúc real-time streaming** — batch training & inference.

### 3. Citation chuẩn IEEE

```
[X] J. Yang and L. Liu, "Robust Anomaly Detection in Financial Markets Using LSTM
    Autoencoders and Generative Adversarial Networks," Engineering Open Access
    (Eng OA), vol. 3, no. 8, pp. 1–11, Aug. 2025.
```
*(DOI chưa được cung cấp trong bản PDF; nguồn: opastpublishers.com)*

### 4. Quote đáng dùng trong gap statement

> *"The reliance on daily-level data, though pragmatic and reproducible, constrains the model's ability to capture microstructure-level patterns such as spoofing or intraday manipulation. We acknowledge that true financial anomalies often emerge at higher frequencies and under nuanced market conditions."*
> — Yang & Liu (2025), Section 7.1

> *"due to cost and access restrictions, our study uses daily-level return and volume data from Yahoo Finance—freely available and more practical for academic and industry use. While sufficient for macro-patterns, this limits the detection of short-lived or intraday anomalies."*
> — Yang & Liu (2025), Section 2.2

### 5. So sánh với ĐATN

| Tiêu chí | Yang & Liu 2025 | ĐATN |
|---|---|---|
| **Thị trường** | Mỹ (38 stocks — indices, mega-cap, penny) | VN30 — thị trường mới nổi Việt Nam |
| **Dữ liệu** | Daily return + volume (Yahoo Finance) | Tick data near real-time (~78k ticks/phiên) |
| **Granularity** | Daily (macro patterns) | Intraday tick level (microstructure patterns) |
| **Phương pháp** | LSTM-AE + OC-SVM + GAN hybrid | Isolation Forest per-stock (lightweight) |
| **Features** | Daily return, volume | OFI, VWAP deviation, volume rolling stats |
| **Đánh giá** | Artificial anomaly injection | Known-Event Validation (sự kiện thực VN) |
| **Kiến trúc** | Batch (Python/TensorFlow/sklearn) | Kafka + PySpark + Delta Lake streaming |
| **Overhead** | High (Deep learning: LSTM + GAN) | Thấp hơn nhiều (IF linear complexity) |

---

## Paper 4 — Liu et al. 2008 (Isolation Forest nguyên gốc)

### 1. Tóm tắt (3–4 câu)

Bài báo gốc đề xuất thuật toán Isolation Forest (iForest) — phương pháp phát hiện bất thường không giám sát dựa trên nguyên lý cô lập (isolation) thay vì xây dựng profile dữ liệu bình thường. Mỗi instance được đánh giá bằng độ dài đường đi trung bình (average path length) trong một tập cây ngẫu nhiên (ensemble of isolation trees); anomaly thường bị cô lập sớm hơn (đường đi ngắn hơn) vì chúng "few and different". Thực nghiệm trên 12 tập dữ liệu thực tế (bao gồm KDD CUP 99 Http với 567.497 instances) cho thấy iForest vượt ORCA, LOF, Random Forest cả về AUC lẫn tốc độ. Thuật toán có độ phức tạp thời gian O(tψ log ψ) tuyến tính, yêu cầu bộ nhớ thấp, phù hợp dữ liệu lớn.

### 2. Hạn chế / Gap (từ chính tác giả và từ design của thuật toán)

- **Không mô hình hóa temporal dependencies** — thuật toán được thiết kế cho dữ liệu tĩnh (static tabular), không có cơ chế nhớ context thời gian.
- **Curse of dimensionality:** *"For iForest, it also suffers from the same 'curse of dimensionality'."* — cần attribute selection khi nhiều feature không liên quan.
- **Swamping và masking** khi anomaly clusters lớn/dày đặc — giảm hiệu suất phát hiện.
- **Không có cơ chế concept drift adaptation** — sub-sampling size cố định, không tự điều chỉnh khi phân phối dữ liệu thay đổi.
- **Không có ứng dụng tài chính nào** trong bài gốc — evaluation chỉ trên UCI/KDD datasets.
- **Không đề cập sliding window retrain** hay incremental learning.
- Anomaly score phụ thuộc vào sub-sampling size ψ — cần tune thực nghiệm.

### 3. Citation chuẩn IEEE

```
[X] F. T. Liu, K. M. Ting, and Z.-H. Zhou, "Isolation Forest," in Proc. 8th IEEE Int. Conf.
    Data Mining (ICDM 2008), Pisa, Italy, Dec. 2008, pp. 413–422,
    doi: 10.1109/ICDM.2008.17.
```

### 4. Quote đáng dùng trong gap statement

> *"For iForest, it also suffers from the same 'curse of dimensionality'."*
> — Liu et al. (2008), Section 5.3

> *"iForest has the capacity to scale up to handle extremely large data size and high-dimensional problems with a large number of irrelevant attributes."*
> — Liu et al. (2008), Section 1 *(điểm mạnh dùng để motivate lựa chọn IF cho tick data)*

> *"Taking advantage of anomalies' nature of 'few and different', iTree isolates anomalies closer to the root of the tree."*
> — Liu et al. (2008), Section 7 *(quote cơ sở lý thuyết)*

### 5. So sánh với ĐATN

| Tiêu chí | Liu et al. 2008 (IF gốc) | ĐATN |
|---|---|---|
| **Bài toán** | General anomaly detection (UCI datasets, network intrusion) | Anomaly detection trong giao dịch tài chính VN |
| **Dữ liệu** | Static tabular (UCI, KDD CUP) | Tick data streaming intraday, time-series |
| **Temporal modeling** | Không có | Features window-based (OFI, VWAP rolling) |
| **Feature engineering** | Raw features | OFI, VWAP deviation, volume z-score rolling |
| **Concept drift** | Không đề cập | Sliding window retrain per phiên |
| **Scale** | Large batch (567k instances) | Streaming ~78k ticks/phiên × 30 stocks |
| **Đánh giá** | AUC trên labeled UCI datasets | Known-Event Validation Framework (VN events) |
| **Kiến trúc** | Standalone algorithm | Integrated vào pipeline Kafka+PySpark+MLflow |
| **Per-stock** | Single global model | Per-stock model — thích ứng với đặc thù từng cổ phiếu VN30 |

> **Nhận xét:** ĐATN kế thừa IF làm core algorithm và mở rộng đáng kể: (1) áp dụng cho tick data tài chính qua feature engineering microstructure; (2) thiết kế per-stock model để nắm bắt đặc thù thanh khoản từng mã VN30; (3) tích hợp sliding window retrain giải quyết concept drift mà bài gốc chưa xét; (4) đưa vào kiến trúc streaming production-grade.

---

## Paper 5 — Lê Hoàng Anh 2024

### 1. Tóm tắt (3–4 câu)

Nghiên cứu ứng dụng phương pháp học máy để xây dựng hệ thống giao dịch cổ phiếu tự động theo chỉ báo kỹ thuật (SMA, Bollinger Bands, RSI, MACD) kết hợp tối ưu danh mục đầu tư theo Sharpe Ratio trên dữ liệu VN30. Quy trình gồm 4 bước: thu thập dữ liệu giá đóng 5 năm (2018–2023), giao dịch tự động theo tín hiệu chỉ báo, tối ưu tỷ trọng danh mục bằng Sharpe ratio, kiểm tra trên dữ liệu 2023. Kết quả cho thấy chiến lược SMA đạt tỷ suất sinh lợi cao nhất 20.94% (2023), danh mục Bollinger Bands đạt Sharpe ratio cao nhất 0.86. Đây là một trong số ít nghiên cứu Việt Nam áp dụng học máy vào giao dịch cổ phiếu VN30.

### 2. Hạn chế / Gap (từ chính tác giả)

- **Phạm vi còn hạn chế:** *"số lượng cổ phiếu, các chỉ báo và phương pháp tối ưu rủi ro cho danh mục còn hạn chế."* — chỉ 5 cổ phiếu/danh mục từ VN30.
- **Chưa mở rộng toàn thị trường:** *"nghiên cứu tiếp theo có thể mở rộng toàn thị trường chứng khoán Việt Nam, kết hợp các chỉ báo trong cùng một chiến lược giao dịch."*
- **Không có phát hiện bất thường** — hoàn toàn tập trung vào tối ưu lợi nhuận, không phát hiện giao dịch bất thường hay cảnh báo rủi ro.
- **Chỉ dùng dữ liệu ngày (daily)** — không có tick data hay intraday analysis.
- **Không có kiến trúc real-time** — offline backtesting, cần "theo dõi, kiểm tra định kỳ (3 tháng, 6 tháng)".
- **Không dùng microstructure features** (không có OFI, VWAP, depth of book).
- **"Phương pháp học máy"** trong bài chỉ là algorithmic trading theo quy tắc chỉ báo — không phải ML model thực sự theo nghĩa statistical learning.
- **Không giải quyết vấn đề cảnh báo sớm** (early warning) hay anomaly detection.

### 3. Citation chuẩn IEEE

```
[X] L. H. Anh and N. L. T. Thy, "Ứng dụng phương pháp học máy trong giao dịch chứng
    khoán theo chỉ báo bằng ngôn ngữ lập trình Python [Applying Machine Learning method
    in stock trading by indicator using Python programming language]," Tạp chí Khoa học
    và Công nghệ - Trường Đại học Bình Dương, vol. 7, no. 1, pp. 47–54, 2024,
    doi: 10.56097/binhduonguniversityjournalofscienceandtechnology.v7i1.212.
```

### 4. Quote đáng dùng trong gap statement

> *"số lượng cổ phiếu, các chỉ báo và phương pháp tối ưu rủi ro cho danh mục còn hạn chế. Nhóm nghiên cứu hi vọng nghiên cứu tiếp theo có thể mở rộng toàn thị trường chứng khoán Việt Nam."*
> — Lê Hoàng Anh & Nguyễn Lê Thanh Thy (2024), Mục 5.1

*(Dùng để chứng minh: nghiên cứu ML trên VN30 còn mới, thiếu mảng phát hiện bất thường)*

### 5. So sánh với ĐATN

| Tiêu chí | Lê Hoàng Anh 2024 | ĐATN |
|---|---|---|
| **Thị trường** | VN30 (cùng thị trường) | VN30 |
| **Mục tiêu** | Tối ưu lợi nhuận danh mục đầu tư | Phát hiện và cảnh báo giao dịch bất thường |
| **Dữ liệu** | Daily closing price, 2018–2023 | Tick data streaming ~78k ticks/phiên |
| **Phương pháp** | Technical indicators + Sharpe Ratio | Isolation Forest + microstructure features |
| **Real-time** | Không — offline backtesting | Có — Kafka + PySpark near real-time |
| **Anomaly detection** | Không | Có — core của hệ thống |
| **Features** | Price, SMA, Bollinger, RSI, MACD | OFI, VWAP deviation, volume rolling stats |
| **Đánh giá** | Tỷ suất sinh lợi so benchmark | Known-Event Validation Framework |
| **Kiến trúc** | Python script + pandas | Kafka + PySpark + Delta Lake + Streamlit |

> **Nhận xét:** Bài báo này quan trọng để chứng minh **gap về phía ứng dụng VN**: nghiên cứu học máy trên VN30 hiện chủ yếu tập trung vào dự báo giá và tối ưu danh mục (Lê Hoàng Anh 2024; Tuyên 2024), **hoàn toàn thiếu vắng** phương pháp phát hiện bất thường giao dịch nội phiên trên dữ liệu tick.

---

## Tổng Hợp: Bảng Gap Matrix

| Paper | Method | Dữ liệu | Hạn chế chính | Điểm ĐATN khác biệt |
|---|---|---|---|---|
| **Poutré et al. 2023** | Transformer-AE + OC-SVM (hybrid deep unsupervised) | LOB L1 tick, 5 NASDAQ stocks, **1 ngày** duy nhất | (1) Chỉ 1 ngày giao dịch, không cross-session; (2) Chỉ thị trường Mỹ; (3) Nhãn synthetic; (4) Chưa giải quyết concept drift/retrain; (5) Không có real-time architecture; (6) Phức tạp tính toán cao | (1) Thị trường VN30 mới nổi, multi-session; (2) Sliding window retrain theo phiên; (3) Known-Event Validation thay synthetic; (4) Kiến trúc Kafka+PySpark production-grade; (5) IF nhẹ hơn Transformer-AE |
| **Núñez et al. 2024** | k-Partitioned Isolation Forest ensemble + voting | Daily/hourly OHLCV, **8 stocks Mỹ (2003)**, 55 labeled blocks | (1) Dữ liệu cũ (2003), daily granularity; (2) IF designed for static data; (3) Precision rất thấp (3–5.5%); (4) Không real-time; (5) Chỉ k≤3; (6) Labeled bởi SEC lawsuits | (1) Tick data intraday VN30; (2) Feature engineering microstructure (OFI, VWAP); (3) Không cần nhãn; (4) Real-time streaming; (5) Per-stock model thích ứng thanh khoản từng mã |
| **Yang & Liu 2025** | LSTM-AE + OC-SVM + GAN hybrid (deep learning) | **Daily** return+volume, 38 US stocks (Yahoo Finance) | (1) Daily data — bỏ lỡ intraday anomaly; (2) Tự thừa nhận tick/LOB tốt hơn nhưng không tiếp cận được; (3) GAN overfit trên tập nhỏ; (4) Không real-time; (5) Artificial anomaly injection | (1) Tick data thực tế, intraday VN30; (2) Microstructure features (OFI, VWAP) — không dùng daily return; (3) Lightweight IF thay deep learning; (4) Known-Event Validation thay injection; (5) Streaming architecture |
| **Liu et al. 2008** | Isolation Forest (iForest) — thuật toán gốc | 12 UCI/KDD datasets (general anomaly detection) | (1) Không có temporal modeling; (2) Không có ứng dụng tài chính; (3) Không có concept drift handling; (4) Curse of dimensionality; (5) Không có sliding window retrain | (1) Mở rộng IF sang tick data tài chính VN; (2) Feature engineering window-based (OFI, VWAP); (3) Per-stock model — thích ứng từng mã; (4) Sliding window retrain per phiên; (5) Tích hợp vào Kafka+PySpark production |
| **Lê Hoàng Anh 2024** | Technical indicators (SMA/Bollinger/RSI/MACD) + Sharpe Ratio portfolio optimization | Daily closing price, **VN30, 2018–2023** | (1) Không có anomaly detection; (2) Chỉ daily data; (3) Offline backtesting, không real-time; (4) Không có microstructure features; (5) Phạm vi chỉ 5 stocks/portfolio | (1) Cùng VN30 nhưng anomaly detection — mảng hoàn toàn khác; (2) Tick data vs daily; (3) Real-time streaming vs offline; (4) OFI/VWAP vs price indicators; (5) Cảnh báo bất thường vs tối ưu lợi nhuận |

---

## Tóm Tắt Gap Statement cho Chương 1

Tổng hợp 5 nghiên cứu trên, có thể xác định **ba khoảng trống nghiên cứu** (research gaps) mà ĐATN này nhắm đến giải quyết:

### Gap 1: Thiếu phương pháp phát hiện bất thường trên tick data VN30 real-time
Các nghiên cứu quốc tế áp dụng LOB/tick data tập trung vào thị trường phát triển (NASDAQ: Poutré 2023) với kiến trúc offline. Nghiên cứu Việt Nam trên VN30 (Lê Hoàng Anh 2024) chỉ tập trung vào dự báo giá/tối ưu danh mục với dữ liệu ngày, **chưa có** hệ thống phát hiện bất thường giao dịch nội phiên trên dữ liệu tick VN30.

### Gap 2: Chưa có framework đánh giá phù hợp với thị trường không có ground truth label
Các nghiên cứu hiện có hoặc dùng synthetic fraud injection (Yang & Liu 2025, Poutré 2023) hoặc dùng nhãn SEC/IIROC (Núñez 2024) — đều không khả thi với thị trường Việt Nam. ĐATN đề xuất **Known-Event Validation Framework** sử dụng các sự kiện thị trường VN đã biết (trading halts, disclosure events) như pseudo-ground-truth.

### Gap 3: Khoảng cách giữa nghiên cứu học thuật và hệ thống production real-time
Kể cả các nghiên cứu dùng tick data (Poutré 2023) đều là offline research, không có kiến trúc streaming production-grade. Việc tích hợp **Kafka + PySpark + Delta Lake + MLflow + Streamlit** trong ĐATN tạo ra một hệ thống giám sát thực tiễn cho HOSE — điều chưa được đề xuất trong các nghiên cứu đã review.

---

## Ghi chú phương pháp luận

- **Năm của Poutré paper**: File PDF đặt tên là "poutre2024" nhưng tài liệu gốc ghi "July 2023" (CISMF Research Paper Series). Citation dùng **2023**.
- **Yang & Liu 2025**: Submitted June 2025, Published August 2025 — paper rất mới; không có DOI chính thức trong PDF, nhà xuất bản là Opast Publishers (Eng OA ISSN: 2993-8643).
- **Liu 2008**: DOI chuẩn là `10.1109/ICDM.2008.17` (IEEE ICDM 2008) — không hiện trong PDF nhưng có thể verify trên IEEE Xplore.
- **Lê Hoàng Anh 2024**: DOI xác nhận qua PDF: `10.56097/binhduonguniversityjournalofscienceandtechnology.v7i1.212`.

---

*File generated: 2026-05-14 | Dùng cho Chương 1 ĐATN — Tổng quan tài liệu và phân tích gap*
