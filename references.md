# references.md — Danh mục tài liệu tham khảo ĐATN

> **Đề tài:** Xây dựng nền tảng quản lý danh sách theo dõi và cảnh báo giao dịch bất thường trong phiên cho cổ phiếu VN30  
> **Cập nhật lần cuối:** 2026-05-15  
> **Quy ước citation:** IEEE (số trong ngoặc vuông [N])  
> **Trạng thái file:** 📄 Cập nhật liên tục sau mỗi lần viết

---

## HƯỚNG DẪN SỬ DỤNG FILE NÀY

| Ký hiệu | Nghĩa |
|---------|-------|
| ✅ PDF có | Đã download, lưu tại `papers/` |
| ⏳ Cần download | Tìm được nhưng chưa có file PDF |
| ❌ Paywall | Cần institutional access |
| ⭐⭐⭐ | Core reference — bắt buộc cite |
| ⭐⭐ | Related — cite khi viết section liên quan |
| ⭐ | Background — tham khảo thêm |

Cột **"Dùng ở đâu"** ghi tên section cụ thể trong báo cáo ĐATN.

---

## MỤC LỤC THEO NHÓM

- [Nhóm A — Nền tảng Isolation Forest](#nhóm-a--nền-tảng-isolation-forest)
- [Nhóm B — Phát hiện bất thường thị trường tài chính](#nhóm-b--phát-hiện-bất-thường-thị-trường-tài-chính)
- [Nhóm C — Order Flow Imbalance (OFI) & Microstructure](#nhóm-c--order-flow-imbalance-ofi--microstructure)
- [Nhóm D — VWAP & Intraday Signal](#nhóm-d--vwap--intraday-signal)
- [Nhóm E — Kiến trúc Streaming Real-time](#nhóm-e--kiến-trúc-streaming-real-time)
- [Nhóm F — Thị trường chứng khoán Việt Nam](#nhóm-f--thị-trường-chứng-khoán-việt-nam)
- [Nhóm G — Phương pháp đánh giá Unsupervised AD](#nhóm-g--phương-pháp-đánh-giá-unsupervised-ad)
- [Nhóm H — Survey & Background](#nhóm-h--survey--background)
- [Nguồn web & tài liệu kỹ thuật](#nguồn-web--tài-liệu-kỹ-thuật)

---

## Nhóm A — Nền tảng Isolation Forest

---

### [1] Liu et al. 2008 — Isolation Forest (Thuật toán gốc)

**Citation IEEE:**
> F. T. Liu, K. M. Ting, and Z.-H. Zhou, "Isolation Forest," in *Proc. 8th IEEE Int. Conf. Data Mining (ICDM 2008)*, Pisa, Italy, Dec. 2008, pp. 413–422, doi: 10.1109/ICDM.2008.17.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Fei Tony Liu, Kai Ming Ting, Zhi-Hua Zhou |
| **Nơi đăng** | IEEE ICDM 2008 |
| **DOI** | 10.1109/ICDM.2008.17 |
| **File PDF** | ✅ `liu2008_isolation_forest.pdf` (252 KB) |
| **Mức liên quan** | ⭐⭐⭐ |
| **Dùng ở đâu** | Chương 2 §2.4 (Phương pháp IF), Chương 3 §3.5 (Thiết kế mô hình) |

**Tóm tắt dùng khi viết:**
Đề xuất Isolation Forest — thuật toán phát hiện bất thường dựa trên nguyên lý *cô lập* (isolation): điểm bất thường có đường đi ngắn hơn trong cây ngẫu nhiên vì chúng "ít và khác biệt". Độ phức tạp O(n log n), không cần nhãn, scale tốt với dữ liệu lớn.

**Quote đáng dùng:**
> *"Taking advantage of anomalies' nature of 'few and different', iTree isolates anomalies closer to the root of the tree."*

**Justify chọn IF cho ĐATN:**
> *"iForest has the capacity to scale up to handle extremely large data size and high-dimensional problems with a large number of irrelevant attributes."*

---

### [2] Hariri et al. 2021 — Extended Isolation Forest

**Citation IEEE:**
> S. Hariri, M. C. Kind, and R. J. Brunner, "Extended Isolation Forest," *IEEE Trans. Knowledge and Data Engineering*, vol. 33, no. 4, pp. 1479–1489, Apr. 2021, doi: 10.1109/TKDE.2019.2947676. arXiv:1811.02141.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Sahand Hariri, Matias Carrasco Kind, Robert J. Brunner |
| **Nơi đăng** | IEEE TKDE, vol. 33, no. 4, 2021 |
| **DOI** | 10.1109/TKDE.2019.2947676 |
| **arXiv** | https://arxiv.org/pdf/1811.02141 |
| **File PDF** | ✅ `papers/hariri2021_EIF.pdf` |
| **Mức liên quan** | ⭐⭐ |
| **Dùng ở đâu** | Chương 2 §2.4 (so sánh EIF vs IF), Chương 3 §3.5 (justify dùng IF chuẩn) |

**Tóm tắt dùng khi viết:**
Mở rộng IF gốc bằng cách cho phép hyperplane cắt với slope ngẫu nhiên thay vì chỉ axis-parallel, giải quyết artifact điểm mù của IF gốc. Liên quan khi phải justify tại sao dùng standard IF thay EIF cho tick data VN30.

---

### [3] Ding & Fei 2013 — iForestASD (IF cho Streaming Data)

**Citation IEEE:**
> Z. Ding and M. Fei, "An Anomaly Detection Approach Based on Isolation Forest Algorithm for Streaming Data Using Sliding Window," *IFAC Proceedings Volumes*, vol. 46, no. 20, pp. 12–17, 2013, doi: 10.3182/20130902-3-CN-3020.00044.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Zhiguo Ding, Minrui Fei |
| **Nơi đăng** | IFAC Proceedings 2013 |
| **DOI** | 10.3182/20130902-3-CN-3020.00044 |
| **Semantic Scholar** | https://www.semanticscholar.org/paper/An-Anomaly-Detection.../d26cfc91... |
| **File PDF** | ✅ `papers/ding2013_iForestASD.pdf` |
| **Mức liên quan** | ⭐⭐⭐ |
| **Dùng ở đâu** | Chương 2 §2.4 (nền tảng sliding window + IF), Chương 3 §3.5 (justify sliding window retrain) |

**Tóm tắt dùng khi viết:**
Đề xuất iForestASD — phương pháp đầu tiên thích ứng Isolation Forest cho streaming data với sliding window để xử lý concept drift. Tiền thân trực tiếp của thiết kế "sliding window retrain per phiên" trong ĐATN.

---

### [4] Togbe et al. 2021 — IF trong Concept-Drifting Streams

**Citation IEEE:**
> M. U. Togbe, Y. Chabchoub, A. Boly, M. Barry, R. Chiky, and M. Bahri, "Anomalies Detection Using Isolation in Concept-Drifting Data Streams," *Computers*, vol. 10, no. 1, p. 13, Jan. 2021, doi: 10.3390/computers10010013.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Muriel Uwase Togbe et al. |
| **Nơi đăng** | MDPI Computers, 2021 (Open Access) |
| **DOI** | 10.3390/computers10010013 |
| **URL** | https://www.mdpi.com/2073-431X/10/1/13 |
| **File PDF** | ✅ `papers/togbe2021_IF_concept_drift.pdf` |
| **Mức liên quan** | ⭐⭐⭐ |
| **Dùng ở đâu** | Chương 2 §2.4 (concept drift + IF), Chương 3 §3.5 (justify sliding window retrain) |

**Tóm tắt dùng khi viết:**
Survey và benchmark các phương pháp IF cho streaming data có concept drift. Cung cấp bằng chứng tại sao sliding window retrain là cần thiết cho financial time series thay đổi liên tục.

---

### [5] Guha et al. 2016 — Robust Random Cut Forest (RRCF)

**Citation IEEE:**
> S. Guha, N. Mishra, G. Roy, and O. Schrijvers, "Robust Random Cut Forest Based Anomaly Detection on Streams," in *Proc. 33rd Int. Conf. Machine Learning (ICML)*, PMLR, vol. 48, 2016, pp. 2712–2721. [Online]. Available: https://proceedings.mlr.press/v48/guha16.html

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Sudipto Guha, Nina Mishra, Gourav Roy, Okke Schrijvers |
| **Nơi đăng** | ICML 2016, PMLR vol. 48 |
| **URL** | https://proceedings.mlr.press/v48/guha16.pdf |
| **File PDF** | ✅ `papers/guha2016_RRCF.pdf` |
| **Mức liên quan** | ⭐⭐ |
| **Dùng ở đâu** | Chương 2 §2.4 (so sánh IF vs RRCF cho streaming) |

**Tóm tắt dùng khi viết:**
RRCF là streaming variant của random forest-based anomaly detection, xử lý concept drift tốt hơn IF gốc. Dùng như baseline so sánh khi justify lựa chọn IF trong ĐATN.

---

## Nhóm B — Phát hiện bất thường thị trường tài chính

---

### [6] Poutré et al. 2023 — Deep Unsupervised AD in High-Frequency Markets

**Citation IEEE:**
> C. Poutré, D. Chételat, and M. Morales, "Deep Unsupervised Anomaly Detection in High-Frequency Markets," *J. Finance Data Sci.*, vol. 10, p. 100129, 2024, doi: 10.1016/j.jfds.2024.100129.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Cédric Poutré, Didier Chételat, Manuel Morales |
| **Nơi đăng** | Journal of Finance and Data Science, vol. 10, 2024 |
| **DOI** | 10.1016/j.jfds.2024.100129 |
| **UQAM PDF** | https://marketsurveillance.esg.uqam.ca/wp-content/uploads/.../Deep-Unsupervised... |
| **File PDF** | ✅ `poutre2024_hfm_anomaly.pdf` (1.6 MB) |
| **Mức liên quan** | ⭐⭐⭐ |
| **Dùng ở đâu** | Chương 1 §1.4 (tình hình nghiên cứu), Chương 2 §2.4, Chương 3 §3.7 (justify Known-Event eval) |

**Tóm tắt dùng khi viết:**
Framework Transformer-AE + OC-SVM cho LOB tick data NASDAQ (5 stocks, 1 ngày), đạt AUROC=0.900 với synthetic fraud. Hạn chế: concept drift chưa giải quyết, chỉ 1 ngày dữ liệu, thị trường Mỹ.

**Quote đáng dùng (gap statement):**
> *"market data drift is an important aspect to consider when deploying any data–based model, because the past learned notion of normality might slowly depart from future normal market behaviors."*

---

### [7] Núñez et al. 2024 — k-Partitioned Isolation Forests

**Citation IEEE:**
> H. Núñez Delafuente, C. A. Astudillo, and D. Díaz, "Ensemble Approach Using k-Partitioned Isolation Forests for the Detection of Stock Market Manipulation," *Mathematics*, vol. 12, no. 9, p. 1336, 2024, doi: 10.3390/math12091336.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Hugo Núñez Delafuente, César A. Astudillo, David Díaz |
| **Nơi đăng** | MDPI Mathematics, vol. 12, no. 9, 2024 |
| **DOI** | 10.3390/math12091336 |
| **URL** | https://www.mdpi.com/2227-7390/12/9/1336 |
| **File PDF** | ✅ `nunez2024_kpartitioned_IF.pdf` (467 KB) |
| **Mức liên quan** | ⭐⭐⭐ |
| **Dùng ở đâu** | Chương 1 §1.4 (tình hình nghiên cứu, so sánh gap), Chương 2 §2.4 |

**Tóm tắt dùng khi viết:**
k-IF ensemble với voting, 8 stocks Mỹ (2003), 55 labeled blocks từ SEC. Recall 89% nhưng precision 3–5.5%. Hạn chế: IF for static data, dữ liệu cũ, daily granularity.

**Quote đáng dùng (gap statement):**
> *"This algorithm, primarily designed for static datasets, necessitated an adaptation to handle time series data effectively."*

---

### [8] Yang & Liu 2025 — LSTM+GAN+OC-SVM

**Citation IEEE:**
> J. Yang and L. Liu, "Robust Anomaly Detection in Financial Markets Using LSTM Autoencoders and Generative Adversarial Networks," *Engineering Open Access*, vol. 3, no. 8, pp. 1–11, Aug. 2025.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | JiAn Yang, Lili Liu |
| **Nơi đăng** | Opast Publishers – Engineering Open Access, 2025 |
| **URL** | https://www.opastpublishers.com/open-access-articles/...9525.html |
| **File PDF** | ✅ `yang_liu2025_lstm_gan.pdf` (2.6 MB) |
| **Mức liên quan** | ⭐⭐⭐ |
| **Dùng ở đâu** | Chương 1 §1.4 (gap: daily data vs tick data), Chương 2 §2.4 |

**Tóm tắt dùng khi viết:**
Hybrid LSTM-AE + OC-SVM + GAN, daily data 38 US stocks. Tự thừa nhận không thể capture intraday microstructure vì giới hạn dữ liệu ngày.

**Quote đáng dùng (gap statement — đây là quote vàng nhất):**
> *"The reliance on daily-level data, though pragmatic and reproducible, constrains the model's ability to capture microstructure-level patterns such as spoofing or intraday manipulation."*

---

### [9] Huynh et al. 2024 — Anomaly Detection for Vietnamese Financial Market

**Citation IEEE:**
> Q. T. Huynh, T. H. Nguyen, D. T. Vu, and M. M. Ngo, "Anomaly Detection For Vietnamese Financial Market," in *Proc. 2024 18th Int. Conf. Advanced Computing and Analytics (ACOMPA)*, Ben Cat, Vietnam, Nov. 2024, pp. 58–62, doi: 10.1109/ACOMPA64883.2024.00016.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Quang Trung Huynh, Thi Huyen Nguyen, Duc Thinh Vu, Minh Man Ngo |
| **Nơi đăng** | ACOMPA 2024, Ben Cat, Vietnam |
| **DOI** | 10.1109/ACOMPA64883.2024.00016 |
| **IEEE Xplore** | https://ieeexplore.ieee.org/document/10818343/ |
| **File PDF** | ✅ `papers/huynh2024_VN_AD.pdf` |
| **Mức liên quan** | ⭐⭐⭐ |
| **Dùng ở đâu** | Chương 1 §1.4 (tình hình nghiên cứu VN — paper gần nhất cùng chủ đề) |

**Tóm tắt dùng khi viết:**
Phát hiện bất thường trong VN30-Index dùng MOIRAI foundation model (Transformer), two-stage: fine-tune trên VN30 rồi tính deviation. Kết quả tốt hơn Bollinger Bands và MAC. Giới hạn: Index-level (không phải từng mã), không có tick data, không có kiến trúc streaming.

> ⚠️ **Cần download** — Tôi không tải được từ IEEE Xplore. Bạn có thể thử truy cập với tài khoản trường hoặc IEEE Xplore để tải `document/10818343`.

---

### [10] Bakumenko & Elragal 2022 — IF vs. các phương pháp unsupervised

**Citation IEEE:**
> A. Bakumenko and A. Elragal, "Detecting Anomalies in Financial Data Using Machine Learning Algorithms," *Systems*, vol. 10, no. 5, p. 130, Aug. 2022, doi: 10.3390/systems10050130.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Alexander Bakumenko, Ahmed Elragal |
| **Nơi đăng** | MDPI Systems, vol. 10, no. 5, 2022 |
| **DOI** | 10.3390/systems10050130 |
| **URL** | https://www.mdpi.com/2079-8954/10/5/130 |
| **File PDF** | ✅ `papers/bakumenko2022_IF_financial.pdf` |
| **Mức liên quan** | ⭐⭐ |
| **Dùng ở đâu** | Chương 2 §2.4 (IF vs supervised vs autoencoders khi không có nhãn) |

**Tóm tắt dùng khi viết:**
So sánh 9 phương pháp (7 supervised + 2 unsupervised) trên tài chính, chứng minh IF hoạt động tốt nhất khi không có nhãn thực. Justify trực tiếp lý do chọn IF trong ĐATN.

---

## Nhóm C — Order Flow Imbalance (OFI) & Microstructure

---

### [11] Cont, Kukanov & Stoikov 2014 — OFI Price Impact (Paper gốc định nghĩa OFI)

**Citation IEEE:**
> R. Cont, A. Kukanov, and S. Stoikov, "The Price Impact of Order Book Events," *J. Financial Econometrics*, vol. 12, no. 1, pp. 47–88, Winter 2014, doi: 10.1093/jjfinec/nbt003.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Rama Cont, Arseniy Kukanov, Sasha Stoikov |
| **Nơi đăng** | Journal of Financial Econometrics, vol. 12, no. 1, 2014 |
| **DOI** | 10.1093/jjfinec/nbt003 |
| **HAL preprint** | https://hal.science/hal-00937055v1 |
| **File PDF** | ✅ `papers/cont2014_OFI_price_impact.pdf` |
| **Mức liên quan** | ⭐⭐⭐ |
| **Dùng ở đâu** | Chương 2 §2.3 (định nghĩa OFI, cơ sở lý thuyết feature) |

**Tóm tắt dùng khi viết:**
Paper gốc định nghĩa OFI = chênh lệch giữa buy pressure và sell pressure tại best bid/ask, chứng minh OFI là yếu tố chính chi phối price impact trong ngắn hạn trên NYSE TAQ data.

**Quote/công thức đáng dùng:**
OFI = Σ[ΔV_bid - ΔV_ask] trong cửa sổ thời gian, với ΔV là thay đổi khối lượng tại mức giá tốt nhất.

---

### [12] Cont, Cucuringu & Zhang 2023 — Cross-Impact of OFI

**Citation IEEE:**
> R. Cont, M. Cucuringu, and C. Zhang, "Cross-Impact of Order Flow Imbalance in Equity Markets," *Quantitative Finance*, 2023, doi: 10.1080/14697688.2023.2236159. arXiv:2112.13213.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Rama Cont, Mihai Cucuringu, Chao Zhang |
| **Nơi đăng** | Quantitative Finance, 2023 |
| **DOI** | 10.1080/14697688.2023.2236159 |
| **arXiv** | https://arxiv.org/pdf/2112.13213 |
| **File PDF** | ✅ `papers/cont2023_cross_OFI.pdf` |
| **Mức liên quan** | ⭐⭐⭐ |
| **Dùng ở đâu** | Chương 2 §2.3 (multi-level OFI, integrated OFI), Chương 3 §3.4 (feature engineering) |

**Tóm tắt dùng khi viết:**
Mở rộng OFI sang multi-level và multi-asset, đề xuất integrated OFI tổng hợp từ nhiều tầng của LOB, cải thiện khả năng giải thích price impact. Nền tảng cho cách tính OFI per cửa sổ 1min/5min trong ĐATN.

---

### [13] Anantha & Jain 2024 — Forecasting HF OFI with Hawkes

**Citation IEEE:**
> A. N. Anantha and S. Jain, "Forecasting High Frequency Order Flow Imbalance," arXiv:2408.03594, Aug. 2024, doi: 10.48550/arXiv.2408.03594.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Aditya Nittur Anantha, Shashi Jain |
| **Nơi đăng** | arXiv preprint, Aug. 2024 |
| **DOI/arXiv** | https://arxiv.org/pdf/2408.03594 |
| **File PDF** | ✅ `papers/anantha2024_HF_OFI.pdf` |
| **Mức liên quan** | ⭐⭐ |
| **Dùng ở đâu** | Chương 2 §2.3 (OFI forecasting, Hawkes process), background |

**Tóm tắt dùng khi viết:**
Dùng Hawkes processes để mô hình hóa OFI trên tick data NSE (Ấn Độ), xử lý lagged dependency giữa buy/sell. Background bổ sung cho phần OFI theory.

---

## Nhóm D — VWAP & Intraday Signal

---

### [14] Zarattini & Aziz 2023 — VWAP Day Trading

**Citation IEEE:**
> C. Zarattini and A. Aziz, "Volume Weighted Average Price (VWAP) The Holy Grail for Day Trading Systems," *SSRN Electronic Journal*, Nov. 2023, doi: 10.2139/ssrn.4631351.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Carlo Zarattini, Andrew Aziz |
| **Nơi đăng** | SSRN Working Paper, 2023 |
| **DOI/SSRN** | https://ssrn.com/abstract=4631351 |
| **File PDF** | ✅ `papers/zarattini2023_VWAP.pdf` |
| **Mức liên quan** | ⭐⭐ |
| **Dùng ở đâu** | Chương 2 §2.3 (lý thuyết VWAP, VWAP deviation làm signal) |

> ⚠️ Lưu ý: SSRN working paper, chưa peer-review. Dùng kèm với citation học thuật hơn khi cần.

**Tóm tắt dùng khi viết:**
Phân tích VWAP deviation như market imbalance signal trong day trading. Cung cấp justification thực tiễn cho feature VWAP deviation trong ĐATN.

---

## Nhóm E — Kiến trúc Streaming Real-time

---

### [15] Carcillo et al. 2018 — SCARFF (Kafka + Spark Fraud Detection)

**Citation IEEE:**
> F. Carcillo, A. Dal Pozzolo, Y.-A. Le Borgne, O. Caelen, Y. Mazzer, and G. Bontempi, "SCARFF: A Scalable Framework for Streaming Credit Card Fraud Detection with Spark," *Information Fusion*, vol. 41, pp. 182–194, May 2018, doi: 10.1016/j.inffus.2017.09.005.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Fabrizio Carcillo et al., Université Libre de Bruxelles |
| **Nơi đăng** | Information Fusion, Elsevier, vol. 41, 2018 |
| **DOI** | 10.1016/j.inffus.2017.09.005 |
| **File PDF** | ✅ `papers/carcillo2018_SCARFF.pdf` |
| **Mức liên quan** | ⭐⭐⭐ |
| **Dùng ở đâu** | Chương 3 §3.1 (kiến trúc tổng thể), §3.2 (thiết kế pipeline Kafka+Spark) |

**Tóm tắt dùng khi viết:**
Thiết kế pipeline Kafka → Spark → Cassandra cho fraud detection real-time trong tài chính, giải quyết đồng thời class imbalance và concept drift trong streaming. Đây là reference kiến trúc production-grade gần nhất với ĐATN.

> ⚠️ **Cần download** — tìm trên ResearchGate hoặc ULB repository. Thông báo nếu không tải được.

---

### [16] Bhatia et al. 2022 — MemStream (Streaming + Concept Drift)

**Citation IEEE:**
> S. Bhatia, A. Jain, S. Srivastava, K. Kawaguchi, and B. Hooi, "MemStream: Memory-Based Streaming Anomaly Detection," in *Proc. ACM Web Conf. (WWW 2022)*, 2022, pp. 1–10, doi: 10.1145/3485447.3512221. arXiv:2106.03837.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Siddharth Bhatia et al., National University of Singapore |
| **Nơi đăng** | ACM WWW 2022 |
| **DOI** | 10.1145/3485447.3512221 |
| **arXiv** | https://arxiv.org/pdf/2106.03837 |
| **File PDF** | ✅ `papers/bhatia2022_memstream.pdf` |
| **Mức liên quan** | ⭐⭐⭐ |
| **Dùng ở đâu** | Chương 2 §2.4 (streaming AD + concept drift), Chương 3 §3.5 |

**Tóm tắt dùng khi viết:**
MemStream dùng denoising autoencoder + memory module để handle concept drift trong streaming mà không cần nhãn. 11 real-world datasets. Background cho xử lý concept drift trong ĐATN.

---

## Nhóm F — Thị trường chứng khoán Việt Nam

---

### [17] Lê Hoàng Anh & Nguyễn Lê Thanh Thy 2024 — Học máy trong giao dịch VN30

**Citation IEEE:**
> L. H. Anh and N. L. T. Thy, "Ứng dụng phương pháp học máy trong giao dịch chứng khoán theo chỉ báo bằng ngôn ngữ lập trình Python," *Tạp chí Khoa học và Công nghệ - Trường Đại học Bình Dương*, vol. 7, no. 1, pp. 47–54, 2024, doi: 10.56097/binhduonguniversityjournalofscienceandtechnology.v7i1.212.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Lê Hoàng Anh, Nguyễn Lê Thanh Thy — Trường Đại học Ngân hàng TP.HCM |
| **Nơi đăng** | Tạp chí KH&CN ĐH Bình Dương, tập 7, số 1, 2024 |
| **DOI** | 10.56097/binhduonguniversityjournalofscienceandtechnology.v7i1.212 |
| **URL** | https://jst.bdu.edu.vn/index.php/jst/article/download/212/171 |
| **File PDF** | ✅ `VN1_le_hoang_anh2024.pdf` (1.4 MB) |
| **Mức liên quan** | ⭐⭐⭐ |
| **Dùng ở đâu** | Chương 1 §1.4 (tình hình nghiên cứu VN), học cách viết văn phong |

**Tóm tắt dùng khi viết:**
Ứng dụng chỉ báo kỹ thuật (SMA, Bollinger, RSI, MACD) + tối ưu Sharpe Ratio trên VN30 2018–2023. Chỉ tập trung tối ưu lợi nhuận, **không có anomaly detection** — đây là gap chính.

---

### [18] Đào Lê Kiều Oanh & Nguyễn Thị Minh Châu 2024 — Dự báo VNIndex bằng học sâu

**Citation IEEE:**
> Đ. L. K. Oanh and N. T. M. Châu, "Dự báo chỉ số chứng khoán bằng học máy: Bằng chứng thực nghiệm từ thị trường chứng khoán Việt Nam," *Tạp chí Kinh tế và Dự báo*, tháng 6/2024. [Online]. Available: https://kinhtevadubao.vn/du-bao-chi-so-chung-khoan-bang-hoc-may-29030.html

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Đào Lê Kiều Oanh, Nguyễn Thị Minh Châu |
| **Nơi đăng** | Tạp chí Kinh tế và Dự báo, tháng 6/2024 |
| **URL** | https://kinhtevadubao.vn/du-bao-chi-so-chung-khoan-bang-hoc-may-29030.html |
| **File PDF** | ⏳ Cần download (web scrape) |
| **Mức liên quan** | ⭐⭐ |
| **Dùng ở đâu** | Chương 1 §1.4 (bối cảnh ML ở VN), học văn phong viết gap statement |

**Tóm tắt dùng khi viết:**
So sánh TCN vs LSTM cho dự báo VNIndex — chứng minh chuỗi thời gian đơn biến, chưa có multi-variable tick features. Pattern viết gap statement rất chuẩn, dùng làm mẫu văn phong.

---

### [19] Nguyễn Thị Thanh Loan và cộng sự 2024 — Phân tích dữ liệu rủi ro tài chính VN

**Citation IEEE:**
> N. T. T. Loan et al., "Nghiên cứu ứng dụng phân tích dữ liệu trong quản trị rủi ro tài chính tại các công ty niêm yết trên sàn chứng khoán Việt Nam," *Tạp chí Kinh tế và Dự báo*, tháng 5/2024. [Online]. Available: https://kinhtevadubao.vn/nghien-cuu-ung-dung-phan-tich-du-lieu-28875.html

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Nguyễn Thị Thanh Loan và cộng sự |
| **Nơi đăng** | Tạp chí Kinh tế và Dự báo, tháng 5/2024 |
| **URL** | https://kinhtevadubao.vn/...28875.html |
| **File PDF** | ⏳ Cần download |
| **Mức liên quan** | ⭐⭐ |
| **Dùng ở đâu** | Học văn phong mô tả kết quả và quy trình nghiên cứu VN chuẩn |

---

### [20] Phuoc et al. 2024 — ML dự báo cổ phiếu VN30

**Citation IEEE:**
> T. Phuoc, P. T. K. Anh, P. H. Tam, and C. V. Nguyen, "Applying Machine Learning Algorithms to Predict the Stock Price Trend in the Stock Market – The Case of Vietnam," *Humanities and Social Sciences Communications*, vol. 11, p. 393, 2024, doi: 10.1057/s41599-024-02807-x.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Tran Phuoc et al. |
| **Nơi đăng** | Humanities and Social Sciences Communications (Palgrave/Nature), 2024 |
| **DOI** | 10.1057/s41599-024-02807-x |
| **URL** | https://www.nature.com/articles/s41599-024-02807-x |
| **File PDF** | ✅ `papers/phuoc2024_ML_VN_stock.pdf` |
| **Mức liên quan** | ⭐⭐ |
| **Dùng ở đâu** | Chương 1 §1.4 (bối cảnh ML cho chứng khoán VN) |

---

### [21] ThS. Nguyễn Thị Ngọc Tú & Hoàng Thị Hường 2026 — Dấu ấn TTCK Việt Nam 2025

**Citation IEEE:**
> T. N. T. Nguyễn and H. T. Hường, "Dấu ấn thị trường chứng khoán Việt Nam năm 2025 và giải pháp trọng tâm năm 2026," *Tạp chí Ngân hàng*, tháng 02/2026. [Online]. Available: https://tapchinganhang.gov.vn/

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | ThS. Nguyễn Thị Ngọc Tú, Hoàng Thị Hường |
| **Nơi đăng** | Tạp chí Ngân hàng, tháng 2/2026 |
| **File PDF** | ⏳ Cần download |
| **Mức liên quan** | ⭐⭐ |
| **Dùng ở đâu** | Chương 1 §1.1 (số liệu thị trường VN — thanh khoản 772 triệu CP/ngày, 23.627 tỷ/ngày), học nhịp câu VN4 |

**Số liệu quan trọng từ paper này:**
- Khối lượng giao dịch bình quân: >772 triệu cổ phiếu/ngày
- Giá trị giao dịch bình quân: >23.627 tỷ đồng/ngày
- Số tài khoản: gần 11,6 triệu tài khoản

---

## Nhóm G — Phương pháp đánh giá Unsupervised AD

---

### [22] Idan 2024 — Unsupervised Validation of AD Models

**Citation IEEE:**
> L. Idan, "Towards Unsupervised Validation of Anomaly-Detection Models," in *Proc. 27th European Conf. Artificial Intelligence (ECAI 2024)*, 2024, pp. 1–8, doi: 10.3233/FAIA240859. arXiv:2410.14579.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Lior Idan |
| **Nơi đăng** | ECAI 2024 |
| **DOI** | 10.3233/FAIA240859 |
| **arXiv** | https://arxiv.org/pdf/2410.14579 |
| **File PDF** | ✅ `papers/idan2024_unsupervised_validation.pdf` |
| **Mức liên quan** | ⭐⭐⭐ |
| **Dùng ở đâu** | Chương 3 §3.7 (justify Known-Event Validation methodology) |

**Tóm tắt dùng khi viết:**
Paradigm tự động validate anomaly detection models khi không có labeled validation set, dùng ensemble agreement như proxy. Trực tiếp justify việc dùng proxy ground truth (known events) trong ĐATN.

---

## Nhóm H — Survey & Background

---

### [23] Darban et al. 2024 — Survey Deep Learning for TS Anomaly Detection

**Citation IEEE:**
> Z. Z. Darban, G. I. Webb, S. Pan, C. C. Aggarwal, and M. Salehi, "Deep Learning for Time Series Anomaly Detection: A Survey," *ACM Computing Surveys*, vol. 57, 2024, doi: 10.1145/3691338. arXiv:2211.05244.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Zahra Zamanzadeh Darban et al., Monash University |
| **Nơi đăng** | ACM Computing Surveys, vol. 57, 2024 |
| **DOI** | 10.1145/3691338 |
| **arXiv** | https://arxiv.org/pdf/2211.05244 |
| **File PDF** | ✅ `papers/darban2024_DL_TS_AD_survey.pdf` |
| **Mức liên quan** | ⭐⭐⭐ |
| **Dùng ở đâu** | Chương 2 §2.4 (survey toàn diện về các phương pháp AD time series) |

**Tóm tắt dùng khi viết:**
Survey toàn diện nhất (2024) về deep learning cho anomaly detection trong time series, phân loại 5 paradigm. Reference survey quan trọng nhất cho toàn bộ phần background ĐATN.

---

### [24] Pang et al. 2021 — Deep Learning for Anomaly Detection: A Review

**Citation IEEE:**
> G. Pang, C. Shen, L. Cao, and A. van den Hengel, "Deep Learning for Anomaly Detection: A Review," *ACM Computing Surveys*, vol. 54, no. 2, Article 38, Mar. 2021, doi: 10.1145/3439950.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Guansong Pang et al., Adelaide + SMU |
| **Nơi đăng** | ACM Computing Surveys, vol. 54, no. 2, 2021 |
| **DOI** | 10.1145/3439950 |
| **SMU author copy** | https://ink.library.smu.edu.sg/cgi/viewcontent.cgi?...3439950.pdf |
| **File PDF** | ✅ `papers/pang2021_DL_AD_review.pdf` |
| **Mức liên quan** | ⭐⭐ |
| **Dùng ở đâu** | Chương 2 §2.4 (background deep learning AD paradigms) |

---

### [25] Park 2024 — LLM Multi-Agent AD Financial Markets

**Citation IEEE:**
> T. Park, "Enhancing Anomaly Detection in Financial Markets with an LLM-based Multi-Agent Framework," arXiv:2403.19735, Mar. 2024, doi: 10.48550/arXiv.2403.19735.

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Taejun Park |
| **Nơi đăng** | arXiv preprint, 2024 |
| **arXiv** | https://arxiv.org/pdf/2403.19735 |
| **File PDF** | ✅ `papers/park2024_LLM_AD_financial.pdf` |
| **Mức liên quan** | ⭐⭐ |
| **Dùng ở đâu** | Chương 4 §4.6 (hướng phát triển — alert verification với LLM) |

---

## Nguồn web & tài liệu kỹ thuật

---

### [W1] vnstock — Thư viện dữ liệu chứng khoán Việt Nam

**Citation IEEE:**
> T. Vu, "vnstock: Vietnamese stock market data for Python" [Phần mềm mã nguồn mở], 2022. [Online]. Available: https://github.com/thinh-vu/vnstock

| Trường | Thông tin |
|--------|-----------|
| **Tác giả** | Thinh Vu |
| **Loại** | Open source library |
| **URL** | https://github.com/thinh-vu/vnstock |
| **Dùng ở đâu** | Chương 3 §3.2 (nguồn dữ liệu tick), Chương 2 §2.5 |

**Ghi chú kỹ thuật quan trọng:**
- KBS source: polling 60s, rate limit 60 req/phút (community API key)
- Thực đo 14/05/2026: ~78.000 ticks/phiên, 30 mã VN30
- FPT: 6.341 ticks/ngày ↔ BCM: 305 ticks/ngày

---

### [W2] Apache Kafka Documentation

**Citation IEEE:**
> Apache Software Foundation, "Apache Kafka Documentation," version 3.x, 2024. [Online]. Available: https://kafka.apache.org/documentation/

| Dùng ở đâu | Chương 3 §3.2 (justify Kafka cho decoupling/buffer) |
|------------|-----------------------------------------------------|

---

### [W3] Delta Lake Documentation — Medallion Architecture

**Citation IEEE:**
> Databricks, "Delta Lake: Open-source storage layer," 2023. [Online]. Available: https://delta.io/

| Dùng ở đâu | Chương 2 §2.5, Chương 3 §3.3 (kiến trúc Medallion Bronze/Silver/Gold) |
|------------|-----------------------------------------------------------------------|

---

### [W4] MLflow Documentation

**Citation IEEE:**
> Databricks, "MLflow: An open-source platform for ML lifecycle," 2024. [Online]. Available: https://mlflow.org/docs/latest/index.html

| Dùng ở đâu | Chương 3 §3.5, §3.7 (experiment tracking, model registry) |
|------------|-------------------------------------------------------------|

---

## BẢNG TỔNG HỢP: Trạng thái PDF

**✅ Đã có đủ — tất cả 22 papers đã upload vào `papers/`**

| # | File | Tên rút gọn |
|---|------|------------|
| 1 | `papers/liu2008_isolation_forest.pdf` | Liu 2008 — Isolation Forest |
| 2 | `papers/hariri2021_EIF.pdf` | Hariri 2021 — Extended IF |
| 3 | `papers/ding2013_iForestASD.pdf` | Ding 2013 — iForestASD |
| 4 | `papers/togbe2021_IF_concept_drift.pdf` | Togbe 2021 — IF Concept Drift |
| 5 | `papers/guha2016_RRCF.pdf` | Guha 2016 — RRCF |
| 6 | `papers/poutre2024_hfm_anomaly.pdf` | Poutré 2024 — HFM Anomaly |
| 7 | `papers/nunez2024_kpartitioned_IF.pdf` | Núñez 2024 — k-Partitioned IF |
| 8 | `papers/yang2025_LSTM_GAN.pdf` | Yang 2025 — LSTM+GAN |
| 9 | `papers/huynh2024_VN_AD.pdf` | Huynh 2024 — VN AD (ACOMPA) |
| 10 | `papers/bakumenko2022_IF_financial.pdf` | Bakumenko 2022 — IF Financial |
| 11 | `papers/cont2014_OFI_price_impact.pdf` | Cont 2014 — OFI Price Impact |
| 12 | `papers/cont2023_cross_OFI.pdf` | Cont 2023 — Cross-OFI |
| 13 | `papers/anantha2024_HF_OFI.pdf` | Anantha 2024 — HF OFI Hawkes |
| 14 | `papers/zarattini2023_VWAP.pdf` | Zarattini 2023 — VWAP |
| 15 | `papers/carcillo2018_SCARFF.pdf` | Carcillo 2018 — SCARFF |
| 16 | `papers/bhatia2022_memstream.pdf` | Bhatia 2022 — MemStream |
| 17 | `papers/le_hoang_anh2024_VN1.pdf` | Lê Hoàng Anh 2024 — VN1 |
| 20 | `papers/phuoc2024_ML_VN_stock.pdf` | Phuoc 2024 — ML VN Stock |
| 22 | `papers/idan2024_unsupervised_validation.pdf` | Idan 2024 — Unsupervised Validation |
| 23 | `papers/darban2024_DL_TS_AD_survey.pdf` | Darban 2024 — DL TS AD Survey |
| 24 | `papers/pang2021_DL_AD_review.pdf` | Pang 2021 — DL AD Review |
| 25 | `papers/park2024_LLM_AD_financial.pdf` | Park 2024 — LLM AD Financial |

> Papers [18] Đào Lê Kiều Oanh, [19] Nguyễn Thị Thanh Loan, [21] ThS. Nguyễn Thị Ngọc Tú chưa có PDF (web-only).

---

## LỊCH SỬ CẬP NHẬT

| Ngày | Thay đổi |
|------|---------|
| 2026-05-14 | Tạo file, thêm 25 tài liệu từ paper_analysis.md + new_papers_to_review.md |
| 2026-05-15 | Upload 22 PDFs vào `papers/`, cập nhật trạng thái tất cả entries |
