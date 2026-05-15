# mega-rule.md — v2.0

> Tài liệu này là **nguồn thống nhất** cho toàn bộ đồ án. Phiên bản v2.0 cập nhật các quyết định kỹ thuật sau quá trình phân tích chuyên sâu, kiểm thử thực tế dữ liệu vnstock, rà soát literature và GitHub ecosystem.  
> Mọi phần viết tiếp theo của báo cáo phải bám đúng tài liệu này.

---

## 0. ĐỊNH NGHĨA CHUNG CỦA ĐỀ TÀI

### 0.1 Tên đề tài chính thức
**Xây dựng nền tảng quản lý danh sách theo dõi và cảnh báo giao dịch bất thường trong phiên cho cổ phiếu VN30**

### 0.2 Bản chất của đề tài
Đây là một **đồ án phân tích dữ liệu lớn định hướng sản phẩm**, kết hợp:
- xử lý dữ liệu giao dịch quy mô lớn theo từng tick,
- phát hiện giao dịch bất thường bằng phương pháp unsupervised,
- xây dựng hệ thống hỗ trợ theo dõi và cảnh báo cho người dùng cuối.

Đề tài **không phải**: dự báo giá, đặt lệnh tự động, chatbot, web CRUD.

Đề tài **là**: hệ thống theo dõi dữ liệu tick trong phiên → tính đặc trưng dòng tiền → phát hiện bất thường → cảnh báo người dùng.

### 0.3 Mục đích
Thị trường chứng khoán Việt Nam tồn tại bất cân xứng thông tin. Nhà đầu tư cá nhân không có công cụ theo dõi dòng tiền intraday của tổ chức. Đề tài xây dựng nền tảng xử lý tick data VN30, bóc tách tín hiệu bất thường trong dòng tiền, hỗ trợ theo dõi chủ động hơn.

### 0.4 Mục tiêu

1. Xây dựng pipeline thu thập và lưu trữ tick data VN30 theo cơ chế **near real-time polling (60 giây/cycle)**, đạt tỷ lệ thất thoát dữ liệu thấp.
2. Tính toán đặc trưng chính: **OFI**, **VWAP deviation**, volume-based features, rolling statistics (1 phút và 5 phút).
3. Huấn luyện mô hình **Isolation Forest (per-stock, sliding window retrain)** phát hiện khung thời gian bất thường.
4. Đánh giá mô hình bằng **Known-Event Validation Framework** (không cần ground truth label).
5. Xây dựng giao diện cảnh báo: watchlist, signal flag, truy vấn trong/sau phiên.

### 0.5 Phạm vi

**Dữ liệu:** Tick data 30 mã VN30 — trường chính: mã, thời gian, giá, khối lượng, hành vi B/S.  
**Thực đo (14/05/2026):** ~78,000 ticks/phiên (30 mã), ~19–25M rows/năm. Phân bố: BCM 305 ticks/ngày ↔ FPT 6,341 ticks/ngày. *(Không phải 37.5M như ước tính ban đầu — document thực đo vào báo cáo.)*

**Kỹ thuật:** Thu thập near real-time, lưu trữ columnar, feature engineering, anomaly detection, OLAP query, API + UI.

**Người dùng:** Nhà đầu tư cá nhân, môi giới, analyst.

**Ngoài phạm vi:** Dự báo giá, đặt lệnh tự động, Level-2 Order Book trả phí, giám sát pháp lý cấp Sở.

---

## 1. BỐ CỤC BÁO CÁO

*(Cập nhật v2.1 — duyệt 2026-05-14)*

### Phần đầu: Bìa, Lời cảm ơn, Lời nói đầu, Danh mục hình/bảng/viết tắt.

### MỞ ĐẦU
- Lý do chọn đề tài
- Bố cục báo cáo

### Chương 1. Giới thiệu đề tài
- 1.1 Đặt vấn đề
- 1.2 Tổng quan tình hình nghiên cứu
  - 1.2.1 Nghiên cứu trên thế giới
  - 1.2.2 Nghiên cứu tại Việt Nam
  - 1.2.3 Khoảng trống nghiên cứu
- 1.3 Mục tiêu đề tài
- 1.4 Phạm vi và giới hạn
- 1.5 Tổng kết chương

### Chương 2. Cơ sở lý thuyết và phương pháp
- 2.1 Thị trường chứng khoán và dữ liệu giao dịch tick
  - 2.1.1 Cơ chế khớp lệnh và loại lệnh trên HOSE
  - 2.1.2 Dữ liệu giao dịch tick và đặc điểm intraday VN30
- 2.2 Giao dịch bất thường trong phiên
  - 2.2.1 Khái niệm và đặc điểm
  - 2.2.2 Thách thức trong môi trường không có nhãn xác thực
- 2.3 Đặc trưng vi cấu trúc thị trường
  - 2.3.1 Chỉ số mất cân bằng dòng lệnh (OFI)
  - 2.3.2 Độ lệch giá bình quân theo khối lượng (VWAP deviation)
  - 2.3.3 Các đặc trưng thống kê cửa sổ trượt
- 2.4 Phát hiện bất thường không giám sát
  - 2.4.1 Tổng quan các phương pháp
  - 2.4.2 Thuật toán Isolation Forest
  - 2.4.3 Xử lý hiện tượng trôi dạt khái niệm (concept drift)
- **2.5 Phương pháp thực hiện**
  - 2.5.1 Kiến trúc tổng thể hệ thống
  - 2.5.2 Quy trình xây dựng và đánh giá mô hình
- 2.6 Các công nghệ sử dụng
- 2.7 Tổng kết chương

### Chương 3. Thiết kế và xây dựng hệ thống
- 3.1 Pipeline thu thập và xử lý dữ liệu luồng
  - 3.1.1 Thu thập dữ liệu tick gần thời gian thực
  - 3.1.2 Xử lý luồng với PySpark Structured Streaming
  - 3.1.3 Lưu trữ theo kiến trúc Medallion
- 3.2 Tính toán đặc trưng dòng tiền
  - 3.2.1 Quy trình tính OFI và VWAP deviation
  - 3.2.2 Thống kê cửa sổ trượt
- 3.3 Mô hình phát hiện bất thường
  - 3.3.1 Mô hình per-stock với cơ chế cửa sổ trượt
  - 3.3.2 Phương pháp đánh giá Known-Event Validation
- 3.4 Giao diện và dịch vụ API
- 3.5 Tổng kết chương

### Chương 4. Thực nghiệm và đánh giá
- 4.1 Môi trường và dữ liệu thực nghiệm
- 4.2 Kết quả pipeline và đặc trưng
- 4.3 Kết quả mô hình phát hiện bất thường
  - 4.3.1 AUROC và kiểm định Mann-Whitney U
  - 4.3.2 Recall@K và độ ổn định contamination
- 4.4 Sản phẩm hoàn thiện
  - 4.4.1 Giao diện danh mục theo dõi và cảnh báo
  - 4.4.2 Hiệu năng truy vấn
- 4.5 Đánh giá ưu điểm, hạn chế và hướng phát triển
- 4.6 Tổng kết chương

### Kết luận | Tài liệu tham khảo | Phụ lục

---

## 2. TECH STACK VÀ KIẾN TRÚC

### 2.1 Nguyên tắc chọn tech stack
1. Phù hợp với dữ liệu lớn hơn Pandas thuần.
2. Triển khai được với tài nguyên sinh viên.
3. Giá trị nghề nghiệp DE/DS/MLOps.
4. Đủ để xây sản phẩm hoàn chỉnh.

### 2.2 Tech stack chốt

| Component | Tool | Vai trò |
|---|---|---|
| Data source | **vnstock (KBS source)** | Intraday tick polling, lịch sử, backfill |
| Orchestration | **Apache Airflow** | Lập lịch, retry, checkpoint |
| Message queue | **Apache Kafka** | Decoupling ingestion/processing, buffer |
| Stream processing | **PySpark Structured Streaming** | Bronze→Silver: consume Kafka, normalize, Delta write |
| Storage | **Delta Lake** | ACID, partition, Z-Ordering |
| Feature engineering | **Dask** | Silver→Gold: OFI/VWAP rolling, sklearn integration |
| ML | **Scikit-learn / Isolation Forest** | Anomaly detection, per-stock, sliding window retrain |
| MLOps | **MLflow** | Experiment tracking, model registry |
| Analytical query | **DuckDB** | OLAP trực tiếp trên Parquet/Delta, low latency |
| Backend | **FastAPI** | Inference endpoint, truy vấn |
| Frontend | **Streamlit** | Dashboard prototype, watchlist, cảnh báo |

### 2.3 Kiến trúc pipeline

```
vnstock.intraday() polling (KBS source, ~60s/cycle)
   ↓  [delta ticks since last_id]
Airflow DAG trigger
   ↓
Kafka Topics (partition theo ticker, 30 topics)
   ↓  [decoupling + buffer — justify: fault isolation, không phải real-time latency]
PySpark Structured Streaming
   ↓  [Bronze: raw normalize → Silver: clean schema]
Delta Lake (Medallion: Bronze / Silver / Gold)
   ↓
Dask Feature Engineering
   ↓  [Silver → Gold: OFI, VWAP_dev, vol_ratio, rolling stats 1min/5min]
Isolation Forest per-stock (sliding window retrain)
   ↓
MLflow (log params, metrics, model artifact)
   ↓
DuckDB → FastAPI → Streamlit Dashboard
```

### 2.4 Justify từng component (câu trả lời cho hội đồng)

**Kafka:**
> *"Kafka không được dùng vì real-time latency. Kafka được dùng vì decoupling ingestion layer khỏi processing layer — khi vnstock bị rate limit (20 req/phút guest, 60 req/phút community), Kafka buffer giữ delta ticks đã fetch mà không block PySpark pipeline. Đây là fault isolation pattern, được validated bởi production implementations tương tự (Sulayam, 2024)."*

**PySpark + Dask (boundary rõ):**
> *"PySpark xử lý ingestion và storage vì cần Structured Streaming + Delta Lake connector. Dask xử lý feature engineering vì integrate trực tiếp với scikit-learn mà không cần JVM serialization overhead — giảm latency và complexity ở feature computation layer."*

**Isolation Forest:**
> *"IF được chọn vì: (1) O(n log n) scale với 20M rows trên CPU, loại bỏ OC-SVM O(n²) và LOF O(n log n) với dimensional degradation; (2) rolling-window feature engineering đã encode temporal context trước khi vào model; (3) contamination parameter là explainable prior domain knowledge; (4) path-length score decompose thành per-feature attribution — cần thiết cho interpretable anomaly explanation; (5) sklearn-native, MLflow.sklearn.log_model() trong một dòng."*

**Streamlit:**
> *"Streamlit phù hợp cho prototype và demo sản phẩm trong phạm vi đồ án. Production deployment sẽ cần React/Next.js frontend với WebSocket real-time update, authentication layer, và horizontal scaling — đây là hướng phát triển tiếp theo sau khi validate product-market fit."*

---

## 3. MÔ HÌNH PHÁT HIỆN BẤT THƯỜNG — CHI TIẾT

### 3.1 Kiến trúc 3 lớp

```
Layer 1 — PRIMARY: Isolation Forest (per-stock)
  n_estimators=200, contamination=0.01–0.05
  Sliding window retrain: re-fit mỗi N phiên mới (handle concept drift)
  Output: anomaly_score ∈ R, anomaly_flag ∈ {-1, 1}

Layer 2 — COMPARISON: Vanilla Autoencoder (2–3 mã đại diện, full year)
  Input/Output: same feature vector (OFI, VWAP_dev, vol_ratio, rolling_stats)
  Metric: reconstruction error
  Mục đích: "IF ∩ AE agree → high-confidence anomaly"

Layer 3 — BASELINE: Rolling Z-Score
  Đơn giản, interpretable
  Mục đích: so sánh IF value-add over simple statistical method
```

### 3.2 Sliding Window Retrain

```python
# Mỗi phiên mới, retrain trên N_WINDOW phiên gần nhất
N_WINDOW = 60  # 60 phiên ~ 3 tháng

for session_date in sorted_session_dates:
    window_data = feature_store.query(
        symbol=sym,
        start=session_date - N_WINDOW,
        end=session_date - 1
    )
    model = IsolationForest(n_estimators=200, contamination=0.02)
    model.fit(window_data[FEATURE_COLS])
    mlflow.sklearn.log_model(model, f"if_{sym}_{session_date}")
```

*Lý do:* Financial time series non-stationary. Model train trên data cũ sẽ drift. Sliding window retrain là established pattern, được dùng trong production (Sulayam, 2024).

### 3.3 Features

| Feature | Cửa sổ | Mô tả |
|---|---|---|
| OFI | 1min, 5min | (buy_vol - sell_vol) / total_vol |
| VWAP_deviation | 1min, 5min | (price - VWAP) / VWAP |
| volume_ratio | 1min, 5min | window_vol / rolling_mean_vol(20) |
| spread_proxy | tick | abs(price_change) / price |
| tick_count | 1min, 5min | số lệnh trong cửa sổ |
| return_zscore | 5min | z-score của return so với 20-period rolling |

---

## 4. EVALUATION FRAMEWORK — KNOWN-EVENT VALIDATION

### 4.1 Lý do không dùng traditional evaluation

Isolation Forest là unsupervised — không có ground truth label. Đây là **đặc điểm chung của toàn bộ financial anomaly detection literature** (Yang & Liu, 2025; Poutré et al., 2023; Núñez et al., 2024). Giải pháp được chấp nhận trong academia là dùng proxy ground truth.

### 4.2 Known-Event Construction (proxy ground truth)

**Nguồn 1 — VN-Index market shock days:**
- VN-Index return < -1.5% hoặc > +1.5%: 29 ngày trong 2024–2025
- Top events thực đo: 2025-04-03 (-6.68%), 2025-04-08 (-6.43%), 2024-04-15 (-4.70%), 2024-08-05 (-3.92%)

**Nguồn 2 — Per-stock shock days:**
- Return > ±4% trong ngày
- Volume > mean + 3σ (rolling 20 ngày)
- Return z-score > ±2.5
- Thực đo: VCB 15 ngày, FPT 19 ngày, HPG 16 ngày

**Nguồn 3 — High-confidence (cross-validated):**
- Ngày vừa market shock vừa stock shock: 27 events (thực đo)
- Đây là tier label mạnh nhất để report

### 4.3 Separation of Concerns — Quan trọng nhất

```
Training:    IF thấy FEATURES, KHÔNG thấy event labels
Evaluation:  Known-event dates dùng để TEST model, không dùng trong training
```

*→ Đây là cách Poutré et al. (2023), Yang & Liu (2025) đều làm. Scientifically sound.*

### 4.4 Metrics (4 lớp)

**Layer A — AUROC:**
- Treat event_days=1, normal_days=0
- Report AUROC trên mean_score, max_score, p90_score
- Target: > 0.65 là acceptable, > 0.70 là good

**Layer B — Mann-Whitney U test (non-parametric):**
- H1: anomaly_score trên event days > normal days (one-tailed)
- p < 0.05 → statistically significant signal

**Layer C — Recall@K:**
- Top-K ngày model flag anomalous nhất
- Bao nhiêu % là known events?
- Report K = 10, 20, 30, 50

**Layer D — Contamination Sensitivity:**
- Test contamination ∈ {0.01, 0.02, 0.05, 0.08, 0.10}
- AUROC std < 0.05 → model stable, không noise-fit

### 4.5 Câu trả lời chuẩn cho hội đồng

> *"Em không có ground truth label cho từng tick — đây là đặc điểm chung của unsupervised anomaly detection trên tài chính (Yang & Liu, 2025; Núñez et al., 2024). Em xây dựng tập known-event dates từ market data công khai: ngày VN-Index biến động trên 1.5% (29 ngày), ngày từng mã có price shock trên 4% hoặc volume spike trên 3-sigma. Isolation Forest được train hoàn toàn unsupervised — model không thấy event labels trong training. Em chỉ dùng event dates ở bước evaluation để kiểm tra model có capture được signal không. Kết quả AUROC, Mann-Whitney p-value, và Recall@K cho thấy mức độ model phân biệt được ngày bất thường so với ngày bình thường."*

---

## 5. DATA VOLUME — SỰ THẬT ĐO ĐƯỢC

### 5.1 Kết quả thực đo (14/05/2026, ~78.8% phiên)

| Mã | Ticks/phiên (đo) | Ước tính cả ngày | Phân loại |
|---|---|---|---|
| FPT | 5,000+ (hit limit) | 6,341+ | 🟢 High |
| BID | 4,087 | 5,183 | 🟢 High |
| SHB | 3,460 | 4,388 | 🟢 High |
| SSI | 2,911 | 3,692 | 🟢 High |
| VCB, MBB, HPG... | 2,000–2,700 | 2,500–3,400 | 🟡 Mid |
| BCM | 241 | 305 | 🔴 Low |
| SAB | 365 | 462 | 🔴 Low |
| SSB | 269 | 341 | 🔴 Low |

**Tổng thực tế:** ~78,000 ticks/phiên × 250 phiên = **~19–25M rows/năm**  
*(Không phải 37.5M như ước tính ban đầu — giáo sư đúng)*

### 5.2 Cách viết trong báo cáo

Ở Section 4.1, thêm bảng thực đo này. Câu defend:  
> *"Pipeline được thiết kế cho worst-case capacity (~37.5M). Volume thực tế ~19–25M rows. Spark justify vì: (1) incremental daily processing trên Delta Lake cần distributed compute ngay cả với 20M rows; (2) pipeline phải scale được khi thêm data source hoặc tăng lịch sử."*

---

## 6. LITERATURE REVIEW — KHOẢNG TRỐNG ĐÃ VERIFIED

### 6.1 Papers liên quan

| Paper | Năm | Method | Data | Evaluation |
|---|---|---|---|---|
| "Anomaly Detection For Vietnamese Financial Market" (IEEE) | 2024–2025 | Chưa rõ (paywall) | **VN30-Index** | Chưa rõ |
| Poutré et al. — Deep Unsupervised Anomaly Detection in HFT | 2023/2024 | Transformer Autoencoder | LOB Level-2 tick (trả phí) | Simulated pump-and-dump |
| Núñez et al. — k-Partitioned Isolation Forests | 2024 | **Ensemble IF biến thể** | Stock market | Unsupervised |
| Yang & Liu — LSTM-AE + GAN + OC-SVM | 2025 | Hybrid LSTM+GAN | Daily OHLCV, 38 US stocks | **Artificial anomaly injection** |
| Springer — IF + CatBoost | 2026 | **Isolation Forest** + CatBoost | Stock subset | Cross-market |

### 6.2 Khoảng trống (Section 1.4 báo cáo)

> *"Các nghiên cứu hiện có tập trung vào daily OHLCV trên thị trường phát triển (Yang & Liu, 2025; Núñez et al., 2024) hoặc Level-2 Order Book trả phí (Poutré et al., 2023). Tại Việt Nam, bước đầu có nghiên cứu phát hiện bất thường trên VN30-Index (IEEE, 2024–2025), nhưng chưa có công trình khai thác tick data intraday cấp từng mã cổ phiếu với đặc trưng OFI/VWAP trong kiến trúc pipeline hiện đại. Đề tài này lấp đầy khoảng trống đó."*

### 6.3 GitHub ecosystem

Không có repo nào kết hợp đủ 5 yếu tố: tick-level stock data + OFI/VWAP features + Isolation Forest + full Kafka/Spark/Delta pipeline + VN30. Bạn đang ở **niche chưa ai implement đầy đủ.**

---

## 7. MLflow — TRACKING STANDARD

```python
with mlflow.start_run(run_name=f"IF_{symbol}_{session_date}"):
    mlflow.log_params({
        "model_type": "IsolationForest",
        "symbol": symbol,
        "n_estimators": 200,
        "contamination": 0.02,
        "window_sessions": 60,
        "features": "OFI_1m,OFI_5m,VWAP_dev_1m,VWAP_dev_5m,vol_ratio,tick_count,return_zscore",
        "n_train_records": len(X_train)
    })
    model = IsolationForest(n_estimators=200, contamination=0.02, n_jobs=-1)
    model.fit(X_train)
    mlflow.log_metrics({
        "anomaly_rate": (flags == -1).mean(),
        "mean_anomaly_score": scores[flags == -1].mean(),
        "score_p1": np.percentile(scores, 1),
        "score_p5": np.percentile(scores, 5),
    })
    mlflow.sklearn.log_model(model, "isolation_forest")
```

---

## 8. KẾ HOẠCH THỰC HIỆN

### 8.1 Tổng thời gian: 8 tuần

### 8.2 Timeline cập nhật

**Tuần 1–2:** Ingestion pipeline
- vnstock KBS polling (đã test: 1.7s/request, 60s/cycle cho 30 mã)
- Airflow DAG + rate limit control (community API key: 60 req/phút)
- Kafka producer per ticker
- Deliverable: pipeline chạy được, data flowing vào Kafka

**Tuần 3–4:** Processing + Storage
- PySpark Structured Streaming consume Kafka → Bronze
- Normalize schema, clean (loại thỏa thuận, fill action) → Silver
- Delta Lake partition by (symbol, date), Z-Ordering
- Deliverable: Silver layer queryable

**Tuần 5–6:** Feature + Model + Evaluation
- Dask: OFI, VWAP_dev, vol_ratio, rolling stats → Gold layer
- Isolation Forest per-stock + sliding window retrain
- **Known-Event construction:** pull VN-Index + per-stock history, flag shock days
- **Evaluation:** AUROC, Mann-Whitney, Recall@K, contamination sensitivity
- MLflow tracking
- Deliverable: model artifact + evaluation report

**Tuần 7:** Serving + Product
- DuckDB OLAP layer
- FastAPI endpoints (watchlist, anomaly flag, score)
- Streamlit dashboard beta
- Deliverable: end-to-end demo chạy được

**Tuần 8:** Polish + Report + Defense
- Streamlit UI hoàn thiện
- Bảng thực đo tick volume vào báo cáo
- Section 3.7 evaluation đầy đủ
- Slide bảo vệ + kịch bản demo
- Deliverable: sản phẩm demo-ready, báo cáo hoàn chỉnh

### 8.3 Milestones

- M1: Data flowing Kafka → Delta Lake
- M2: Feature store (Gold layer) queryable
- M3: Model trained + evaluated (known-event validation done)
- M4: API + Dashboard beta
- M5: Full demo + báo cáo hoàn chỉnh

### 8.4 Rủi ro và xử lý

| Rủi ro | Xử lý |
|---|---|
| vnstock rate limit (20 req/phút guest) | Đăng ký API key miễn phí (60 req/phút), sleep 0.5s/request |
| FPT/BID hit page limit 5,000 | get_all=True + pagination, document limitation |
| Tràn bộ nhớ | PySpark cho processing, Dask lazy eval cho feature, DuckDB cho query |
| Model drift theo thời gian | Sliding window retrain (60-session window) |
| Known-event list quá nhỏ | Mở rộng: thêm mã, thêm event criteria (earnings, circuit breaker) |
| Sản phẩm bị thành dashboard minh họa | Bắt buộc: watchlist functional, API live, anomaly signal có lịch sử |

---

## 9. CÁC NGUYÊN TẮC BẤT BIẾN

1. Không dùng "nội phiên" → dùng "giao dịch trong phiên", "cảnh báo trong phiên".
2. Không gọi đề tài là "dự báo giá".
3. Không mở rộng sang thao túng thị trường như mục tiêu chính.
4. Volume thực tế là ~19–25M rows, không phải 37.5M — document trung thực.
5. Kafka justify bằng decoupling/buffer pattern, không phải real-time latency.
6. PySpark = Bronze→Silver. Dask = Silver→Gold. Boundary phải rõ trong diagram.
7. Evaluation phải có 4 metrics (AUROC, Mann-Whitney, Recall@K, stability).
8. Streamlit = prototype — acknowledge limitation trong Section 4.6.
9. Sliding window retrain phải được document như một design decision.
10. Literature citation: Yang & Liu (2025), Núñez et al. (2024), Poutré et al. (2023), IEEE VN (2024–2025).

---

## 10. CHỐT CUỐI CÙNG

Đồ án được hiểu và triển khai theo định nghĩa sau:

> Đây là đồ án xây dựng nền tảng quản lý danh sách theo dõi và cảnh báo giao dịch bất thường trong phiên cho cổ phiếu VN30, dựa trên tick data quy mô lớn (~19–25M rows/năm), xử lý bằng pipeline near real-time hiện đại (Kafka + PySpark + Delta Lake), tính toán đặc trưng dòng tiền (OFI, VWAP) bằng Dask, áp dụng Isolation Forest với sliding window retrain và Known-Event Validation Framework, phục vụ người dùng qua FastAPI + Streamlit.

**Đây là khoảng trống nghiên cứu thực, chưa có repo hay paper nào implement đầy đủ tất cả các yếu tố này cho thị trường Việt Nam.**

---

*mega-rule v2.0 — cập nhật sau phân tích chuyên sâu, kiểm thử thực tế vnstock (14/05/2026), rà soát literature (5 papers) và GitHub ecosystem (6+ repos)*
