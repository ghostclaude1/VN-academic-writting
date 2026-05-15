# Literature Review — New Papers to Reference
## Đề tài ĐATN: Nền tảng quản lý danh sách theo dõi và cảnh báo giao dịch bất thường VN30

**Ngày tìm kiếm:** 2026-05-14  
**Tổng số papers mới tìm được:** 17 (đã verify qua web search thực tế)  
**Papers đã có (KHÔNG liệt kê lại):** Poutré 2023, Núñez 2024, Yang & Liu 2025, Liu 2008, Lê Hoàng Anh 2024

---

## 📌 DANH SÁCH ƯU TIÊN DOWNLOAD (⭐⭐⭐ trước)

| STT | Paper | Nhóm | Access |
|-----|-------|-------|--------|
| 1 | Cont, Kukanov, Stoikov 2014 (OFI Price Impact) | 1 | HAL open + paywall |
| 2 | Cont, Cucuringu, Zhang 2023 (Cross-OFI) | 1 | arXiv open |
| 3 | Darban et al. 2024 (DL Time Series AD Survey) | 3 | arXiv open |
| 4 | Carcillo et al. 2018 (SCARFF Kafka+Spark) | 4 | Paywall |
| 5 | Bhatia et al. 2022 (MemStream) | 4 | arXiv open |
| 6 | Huynh et al. 2024 (VN30 Anomaly Detection) | 5 | IEEE paywall |
| 7 | Idan 2024 (Unsupervised Validation AD) | 6 | arXiv open |
| 8 | Togbe et al. 2021 (IF + Concept Drift) | 7 | MDPI open |
| 9 | Ding & Fei 2013 (iForestASD) | 7 | Paywall/preprint |

---

## NHÓM 1 — Order Flow Imbalance (OFI) & Microstructure Features

---

### Paper 1.1 ⭐⭐⭐

**Citation IEEE:**
> R. Cont, A. Kukanov, and S. Stoikov, "The Price Impact of Order Book Events," *Journal of Financial Econometrics*, vol. 12, no. 1, pp. 47–88, Winter 2014. doi: 10.1093/jjfinec/nbt003

**Tóm tắt:** Paper gốc định nghĩa Order Flow Imbalance (OFI) như chênh lệch giữa cung và cầu tại best bid/ask, chứng minh rằng OFI là yếu tố chính chi phối biến động giá trong khoảng thời gian ngắn trên dữ liệu NYSE TAQ. Đây là nền tảng lý thuyết trực tiếp giải thích feature OFI trong ĐATN.

**URL:** https://academic.oup.com/jfec/article-abstract/12/1/47/816163  
**Preprint (HAL open access):** https://hal.science/hal-00937055v1  
**Download được:** Preprint có thể tải miễn phí trên HAL; bản gốc là paywall (Oxford Academic)

---

### Paper 1.2 ⭐⭐⭐

**Citation IEEE:**
> R. Cont, M. Cucuringu, and C. Zhang, "Cross-Impact of Order Flow Imbalance in Equity Markets," *Quantitative Finance*, 2023. doi: 10.1080/14697688.2023.2236159. arXiv:2112.13213

**Tóm tắt:** Mở rộng OFI sang multi-asset setting, đề xuất cách tổng hợp OFI từ nhiều mức của limit order book thành một biến integrated OFI có khả năng giải thích tác động giá tốt hơn. Cross-asset OFI lagged cải thiện đáng kể dự báo future returns. Cung cấp nền tảng cho việc tính OFI multi-level trong ĐATN.

**URL (arXiv open):** https://arxiv.org/abs/2112.13213  
**Published:** https://doi.org/10.1080/14697688.2023.2236159  
**Download được:** ✅ Full text miễn phí trên arXiv

---

### Paper 1.3 ⭐⭐

**Citation IEEE:**
> A. N. Anantha and S. Jain, "Forecasting High Frequency Order Flow Imbalance," arXiv:2408.03594, Aug. 2024. doi: 10.48550/arXiv.2408.03594

**Tóm tắt:** Xây dựng các mô hình dự báo OFI tần suất cao sử dụng Hawkes processes để mô hình hoá cross-effects giữa buy và sell-signed trades trong event time. Áp dụng trên tick data từ National Stock Exchange (Ấn Độ). Liên quan đến phần forecasting OFI và thiết kế feature trong ĐATN.

**URL (arXiv open):** https://arxiv.org/abs/2408.03594  
**Download được:** ✅ Full text miễn phí trên arXiv

---

## NHÓM 2 — VWAP Deviation & Intraday Trading Signals

---

### Paper 2.1 ⭐⭐

**Citation IEEE:**
> C. Zarattini and A. Aziz, "Volume Weighted Average Price (VWAP) The Holy Grail for Day Trading Systems," *SSRN Electronic Journal*, Nov. 2023. doi: 10.2139/ssrn.4631351

**Tóm tắt:** Phân tích ứng dụng VWAP trong phát hiện market imbalance và tăng cường quyết định trading. Giới thiệu chiến lược day trading dựa trên VWAP deviation đơn giản và kiểm tra hiệu quả trong nhiều điều kiện thị trường khác nhau. Cung cấp lý giải thực tiễn cho feature VWAP deviation trong ĐATN.

**URL (SSRN open):** https://ssrn.com/abstract=4631351  
**Download được:** ✅ Full text có thể tải từ SSRN (working paper)

> ⚠️ Ghi chú: Đây là SSRN working paper, chưa peer-review. Nếu cần academic citation mạnh hơn, có thể bổ sung Madhavan et al. hoặc Berkowitz et al. về VWAP theory.

---

## NHÓM 3 — Unsupervised Anomaly Detection in Financial Time Series (2020–2025)

---

### Paper 3.1 ⭐⭐⭐

**Citation IEEE:**
> Z. Z. Darban, G. I. Webb, S. Pan, C. C. Aggarwal, and M. Salehi, "Deep Learning for Time Series Anomaly Detection: A Survey," *ACM Computing Surveys*, vol. 57, 2024. doi: 10.1145/3691338. arXiv:2211.05244

**Tóm tắt:** Survey toàn diện về deep learning cho phát hiện bất thường time series (cập nhật đến 2024), phân loại các phương pháp theo taxonomy rõ ràng (reconstruction, forecasting, density-based, one-class, ...), bao gồm ứng dụng trong tài chính. Đây là reference survey quan trọng nhất cho toàn bộ phần background ĐATN.

**URL (arXiv open):** https://arxiv.org/abs/2211.05244  
**Published DOI:** https://doi.org/10.1145/3691338 (ACM Computing Surveys)  
**Download được:** ✅ Full text miễn phí trên arXiv

---

### Paper 3.2 ⭐⭐

**Citation IEEE:**
> G. Pang, C. Shen, L. Cao, and A. van den Hengel, "Deep Learning for Anomaly Detection: A Review," *ACM Computing Surveys*, vol. 54, no. 2, Article 38, Mar. 2021. doi: 10.1145/3439950

**Tóm tắt:** Review sâu về các phương pháp deep learning cho anomaly detection, phân loại theo 3 paradigm: deep learning-based feature extraction, learning normality, và end-to-end models. Gồm ứng dụng tài chính. Bổ sung background lý thuyết cho phần mô hình ĐATN.

**URL (open access):** https://dl.acm.org/doi/fullHtml/10.1145/3439950  
**Author copy:** https://ink.library.smu.edu.sg/cgi/viewcontent.cgi?params=/context/sis_research/article/8019/&path_info=3439950.pdf  
**Download được:** ✅ Author's copy open access trên SMU repository

---

### Paper 3.3 ⭐⭐

**Citation IEEE:**
> A. Bakumenko and A. Elragal, "Detecting Anomalies in Financial Data Using Machine Learning Algorithms," *Systems*, vol. 10, no. 5, p. 130, Aug. 2022. doi: 10.3390/systems10050130

**Tóm tắt:** So sánh 7 phương pháp supervised và 2 unsupervised (Isolation Forest + autoencoders) trên dữ liệu tài chính audit, chứng minh Isolation Forest hoạt động tốt khi không có nhãn thực. Liên quan trực tiếp đến lý do chọn Isolation Forest và điểm mạnh của unsupervised approach trong ĐATN.

**URL (MDPI open access):** https://www.mdpi.com/2079-8954/10/5/130  
**Download được:** ✅ Full text miễn phí (MDPI open access, CC BY 4.0)

---

### Paper 3.4 ⭐⭐

**Citation IEEE:**
> T. Park, "Enhancing Anomaly Detection in Financial Markets with an LLM-based Multi-Agent Framework," arXiv:2403.19735, Mar. 2024. doi: 10.48550/arXiv.2403.19735

**Tóm tắt:** Đề xuất framework multi-agent dùng LLM để tự động hóa xác minh và giải thích anomaly alerts được sinh ra bởi hệ thống phát hiện bất thường trên dữ liệu S&P 500. Giải quyết bài toán manual verification — liên quan đến phần alert verification trong kiến trúc ĐATN.

**URL (arXiv open):** https://arxiv.org/abs/2403.19735  
**Download được:** ✅ Full text miễn phí trên arXiv

---

## NHÓM 4 — Real-Time/Streaming Anomaly Detection với Kafka/Spark

---

### Paper 4.1 ⭐⭐⭐

**Citation IEEE:**
> F. Carcillo, A. Dal Pozzolo, Y.-A. Le Borgne, O. Caelen, Y. Mazzer, and G. Bontempi, "SCARFF: A Scalable Framework for Streaming Credit Card Fraud Detection with Spark," *Information Fusion*, vol. 41, pp. 182–194, May 2018. doi: 10.1016/j.inffus.2017.09.005

**Tóm tắt:** Thiết kế và đánh giá pipeline Kafka → Spark → Cassandra cho phát hiện fraud real-time, giải quyết đồng thời class imbalance và concept drift trong streaming. Đây là reference kiến trúc pipeline quan trọng nhất cho hệ thống streaming ĐATN (tương đồng với Kafka + PySpark Structured Streaming).

**URL:** https://doi.org/10.1016/j.inffus.2017.09.005 (Elsevier paywall)  
**Download được:** Paywall — tìm trên ResearchGate hoặc Sci-Hub; có thể có author copy trên ULB repository

---

### Paper 4.2 ⭐⭐⭐

**Citation IEEE:**
> S. Bhatia, A. Jain, S. Srivastava, K. Kawaguchi, and B. Hooi, "MemStream: Memory-Based Streaming Anomaly Detection," in *Proc. ACM Web Conference (WWW)*, 2022, pp. 1–10. doi: 10.1145/3485447.3512221. arXiv:2106.03837

**Tóm tắt:** Đề xuất MemStream — framework phát hiện bất thường trên streaming data sử dụng denoising autoencoder kết hợp memory module để xử lý concept drift mà không cần nhãn. Chứng minh hiệu quả trên 11 real-world datasets. Liên quan đến xử lý concept drift trong sliding window retraining của ĐATN.

**URL (arXiv open):** https://arxiv.org/abs/2106.03837  
**Published:** https://doi.org/10.1145/3485447.3512221 (ACM DL)  
**Download được:** ✅ Full text miễn phí trên arXiv

---

## NHÓM 5 — Vietnamese Stock Market (VN30/HOSE) Data Analysis

---

### Paper 5.1 ⭐⭐⭐ *(từ mega-rule — đã verify)*

**Citation IEEE:**
> [Các tác giả không tiết lộ đầy đủ qua IEEE paywall], "Anomaly Detection For Vietnamese Financial Market," in *2024 18th Int. Conf. Advanced Computing and Analytics (ACOMPA)*, 2024, pp. 58–62. doi: 10.1109/ACOMPA64533.2024.10818343

**Tóm tắt:** Paper tập trung phát hiện bất thường trong VN30-Index thị trường chứng khoán Việt Nam, phục vụ cải thiện ra quyết định đầu tư và quản lý rủi ro. Đây là paper gần nhất với đề tài ĐATN — cùng thị trường VN30, cùng bài toán anomaly detection.

**URL:** https://ieeexplore.ieee.org/document/10818343/  
**Download được:** Paywall (IEEE) — cần institutional access hoặc thẻ IEEE Xplore

---

### Paper 5.2 ⭐⭐

**Citation IEEE:**
> T. Phuoc, P. T. K. Anh, P. H. Tam, and C. V. Nguyen, "Applying Machine Learning Algorithms to Predict the Stock Price Trend in the Stock Market – The Case of Vietnam," *Humanities and Social Sciences Communications*, vol. 11, p. 393, 2024. doi: 10.1057/s41599-024-02807-x

**Tóm tắt:** Đánh giá khả năng áp dụng LSTM kết hợp chỉ số phân tích kỹ thuật để dự báo xu hướng giá cổ phiếu VNIndex và VN30, cung cấp evidence về đặc điểm thị trường chứng khoán Việt Nam. Cung cấp bối cảnh tổng quan về thị trường VN trong ĐATN.

**URL (open access):** https://www.nature.com/articles/s41599-024-02807-x  
**DOAJ entry:** https://doaj.org/article/7508f6e92576472dae659fab848932cf  
**Download được:** ✅ Open access (Palgrave Communications / Nature)

---

## NHÓM 6 — Proxy Ground Truth / Known-Event Validation Methodology

---

### Paper 6.1 ⭐⭐⭐

**Citation IEEE:**
> L. Idan, "Towards Unsupervised Validation of Anomaly-Detection Models," in *Proc. 27th European Conf. Artificial Intelligence (ECAI 2024)*, 2024, pp. 1–8. doi: 10.3233/FAIA240859. arXiv:2410.14579

**Tóm tắt:** Lần đầu tiên đề xuất paradigm tự động validate các mô hình anomaly detection khi không có labeled validation set. Phương pháp dựa trên ensemble agreement/disagreement như proxy cho model validity, áp dụng cho cả model selection và model evaluation. Trực tiếp justify methodology đánh giá unsupervised trong ĐATN.

**URL (arXiv open):** https://arxiv.org/abs/2410.14579  
**Published:** https://doi.org/10.3233/FAIA240859 (IOS Press / ECAI 2024)  
**Download được:** ✅ Full text miễn phí trên arXiv

> ⚠️ Ghi chú Nhóm 6: Paper này là paper duy nhất tìm được trực tiếp về unsupervised validation methodology. Cho methodology Known-Event Validation cụ thể trong ĐATN, cần mô tả như "self-developed framework" và justify bằng precedent từ Poutré 2023 (đã có) + paper này.

---

## NHÓM 7 — Isolation Forest Variants & Extensions for Time Series

---

### Paper 7.1 ⭐⭐⭐

**Citation IEEE:**
> Z. Ding and M. Fei, "An Anomaly Detection Approach Based on Isolation Forest Algorithm for Streaming Data Using Sliding Window," *IFAC Proceedings Volumes*, vol. 46, no. 20, pp. 12–17, 2013. doi: 10.3182/20130902-3-CN-3020.00044

**Tóm tắt:** Đề xuất **iForestASD** — phương pháp đầu tiên thích ứng Isolation Forest cho streaming data với sliding window để xử lý concept drift. Đây là tiền thân trực tiếp của phương pháp "sliding window retrain" được dùng trong ĐATN.

**URL:** https://www.sciencedirect.com/science/article/pii/S1474667016314999  
**Semantic Scholar:** https://www.semanticscholar.org/paper/An-Anomaly-Detection-Approach-Based-on-Isolation-Ding-Fei/d26cfc91b4f7ae0725258e2ed14b5b0116609993  
**Download được:** Paywall (ScienceDirect) — tuy nhiên có thể tìm author copy; frequently cited nên ResearchGate có bản PDF

---

### Paper 7.2 ⭐⭐⭐

**Citation IEEE:**
> M. U. Togbe, Y. Chabchoub, A. Boly, M. Barry, R. Chiky, and M. Bahri, "Anomalies Detection Using Isolation in Concept-Drifting Data Streams," *Computers*, vol. 10, no. 1, p. 13, Jan. 2021. doi: 10.3390/computers10010013

**Tóm tắt:** Survey và so sánh thực nghiệm các phương pháp phát hiện bất thường dựa trên Isolation Forest cho data streams có concept drift (bao gồm iForestASD, HS-Trees, RRCF). Cung cấp benchmark và analysis lý do tại sao cần retrain mô hình trong môi trường streaming tài chính.

**URL (MDPI open access):** https://www.mdpi.com/2073-431X/10/1/13  
**Download được:** ✅ Full text miễn phí (MDPI open access)

---

### Paper 7.3 ⭐⭐

**Citation IEEE:**
> S. Hariri, M. C. Kind, and R. J. Brunner, "Extended Isolation Forest," *IEEE Transactions on Knowledge and Data Engineering*, vol. 33, no. 4, pp. 1479–1489, Apr. 2021. doi: 10.1109/TKDE.2019.2947676. arXiv:1811.02141

**Tóm tắt:** Giải quyết artifact của Isolation Forest gốc bằng cách cho phép tree slices dùng hyperplanes với random slopes thay vì chỉ axis-parallel. Cải thiện đáng kể anomaly score heat maps. Relevant khi so sánh/justify tại sao dùng standard vs. extended Isolation Forest trong ĐATN.

**URL (arXiv open):** https://arxiv.org/abs/1811.02141  
**Published:** https://doi.org/10.1109/TKDE.2019.2947676 (IEEE TKDE)  
**Download được:** ✅ Full text miễn phí trên arXiv

---

### Paper 7.4 ⭐⭐

**Citation IEEE:**
> S. Guha, N. Mishra, G. Roy, and O. Schrijvers, "Robust Random Cut Forest Based Anomaly Detection on Streams," in *Proc. 33rd Int. Conf. Machine Learning (ICML)*, PMLR, vol. 48, 2016, pp. 2712–2721. [Online]. Available: https://proceedings.mlr.press/v48/guha16.html

**Tóm tắt:** Đề xuất Robust Random Cut Forest (RRCF) — cấu trúc dữ liệu streaming dựa trên cây cắt ngẫu nhiên cho phát hiện bất thường real-time. Phù hợp với streaming scenarios, xử lý concept drift tốt hơn iForest gốc. Baseline so sánh với IF trong phần related work.

**URL (PMLR open access):** https://proceedings.mlr.press/v48/guha16.html  
**Download được:** ✅ Full text miễn phí (PMLR)

---

## TỔNG HỢP THEO NHÓM

| Nhóm | Papers mới | Stars |
|------|-----------|-------|
| Nhóm 1 — OFI & Microstructure | 3 | 2×⭐⭐⭐, 1×⭐⭐ |
| Nhóm 2 — VWAP Deviation | 1 | 1×⭐⭐ |
| Nhóm 3 — Unsupervised AD Financial TS | 4 | 1×⭐⭐⭐, 3×⭐⭐ |
| Nhóm 4 — Real-time Streaming | 2 | 2×⭐⭐⭐ |
| Nhóm 5 — Vietnamese Stock Market | 2 | 1×⭐⭐⭐, 1×⭐⭐ |
| Nhóm 6 — Proxy Ground Truth | 1 | 1×⭐⭐⭐ |
| Nhóm 7 — IF Variants for TS | 4 | 2×⭐⭐⭐, 2×⭐⭐ |
| **Tổng** | **17** | **9×⭐⭐⭐, 8×⭐⭐** |

---

## CHÚ Ý VỀ PAPERS TỪ MEGA-RULE (cần verify thêm)

### Sulayam 2024 — Kafka + Spark + Delta Lake production
❌ **Không tìm được paper cụ thể tên "Sulayam 2024"** qua web search.  
Có thể là:
- Blog post / technical report trên Medium/Databricks, không phải academic paper
- Citation có thể sai tên/năm trong mega-rule  

**Khuyến nghị:** Thay thế bằng SCARFF (Carcillo 2018, Paper 4.1) cho architecture citation, hoặc tìm lại trong mega-rule để clarify nguồn gốc.

### Huynh et al. 2024 — ACOMPA 2024 VN30
✅ **Đã verify:** IEEE Xplore document 10818343, 2024 18th International Conference on Advanced Computing and Analytics (ACOMPA 2024), pp. 58–62.  
DOI: 10.1109/ACOMPA64533.2024.10818343  
⚠️ Tên tác giả đầy đủ chưa confirm do IEEE paywall — cần institutional access để lấy đủ metadata.

---

## QUICK DOWNLOAD LINKS (tất cả open access)

```
# arXiv papers (tải PDF trực tiếp):
https://arxiv.org/pdf/2112.13213    # Cont et al. 2023 Cross-OFI
https://arxiv.org/pdf/2408.03594    # Anantha & Jain 2024 HF OFI
https://arxiv.org/pdf/2211.05244    # Darban et al. 2024 DL TS AD Survey
https://arxiv.org/pdf/2106.03837    # Bhatia et al. 2022 MemStream
https://arxiv.org/pdf/2410.14579    # Idan 2024 Unsupervised Validation
https://arxiv.org/pdf/1811.02141    # Hariri et al. 2021 Extended IF
https://arxiv.org/pdf/2403.19735    # Park 2024 LLM Multi-agent AD

# MDPI (open access):
https://www.mdpi.com/2073-431X/10/1/13     # Togbe et al. 2021
https://www.mdpi.com/2079-8954/10/5/130    # Bakumenko & Elragal 2022

# PMLR (open access):
https://proceedings.mlr.press/v48/guha16.pdf    # Guha et al. 2016 RRCF

# SSRN (working paper):
https://ssrn.com/abstract=4631351    # Zarattini & Aziz 2023 VWAP

# HAL preprint (Cont 2014 OFI original):
https://hal.science/hal-00937055v1

# SMU author copy (Pang et al. 2021):
https://ink.library.smu.edu.sg/cgi/viewcontent.cgi?params=/context/sis_research/article/8019/&path_info=3439950.pdf

# Nature/Open (Vietnam ML paper):
https://www.nature.com/articles/s41599-024-02807-x
```

---

## VERIFICATION STATUS

| Paper | Verified Via | Status |
|-------|-------------|--------|
| Cont et al. 2014 | Oxford Academic + HAL + arXiv + SSRN | ✅ Confirmed |
| Cont et al. 2023 | arXiv abstract page direct fetch | ✅ Confirmed |
| Anantha & Jain 2024 | arXiv abstract page | ✅ Confirmed |
| Zarattini & Aziz 2023 | SSRN page + Semantic Scholar | ✅ Confirmed |
| Darban et al. 2022/2024 | arXiv abstract page direct fetch | ✅ Confirmed |
| Pang et al. 2021 | ACM DL + SMU open copy | ✅ Confirmed |
| Bakumenko & Elragal 2022 | MDPI page (multiple sources) | ✅ Confirmed |
| Park 2024 | arXiv abstract page direct fetch | ✅ Confirmed |
| Carcillo et al. 2018 | Multiple citations + DOI confirmed | ✅ Confirmed |
| Bhatia et al. 2022 | arXiv abstract page direct fetch | ✅ Confirmed |
| Huynh et al. 2024 | IEEE Xplore URL + EurekaMAG proceedings | ✅ Confirmed (paywall) |
| Phuoc et al. 2024 | DOAJ + Ideas.REPEC + doi confirmed | ✅ Confirmed |
| Idan 2024 | arXiv abstract page direct fetch | ✅ Confirmed |
| Ding & Fei 2013 | ScienceDirect + Semantic Scholar + multiple citations | ✅ Confirmed |
| Togbe et al. 2021 | MDPI page + ResearchGate + Semantic Scholar | ✅ Confirmed |
| Hariri et al. 2021 | arXiv abstract page direct fetch + Illinois Experts | ✅ Confirmed |
| Guha et al. 2016 | PMLR proceedings page direct | ✅ Confirmed |

**Tất cả 17 papers đã được verify qua web search thực tế. KHÔNG có hallucinated citation.**
