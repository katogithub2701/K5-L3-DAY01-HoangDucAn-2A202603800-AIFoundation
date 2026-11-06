# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV:** 2A202603800
- **Họ và tên:** Hoàng Đức An
- **SEED** (in ở ô đầu notebook): 997

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | ☐ |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | ☐ |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | ☐ |

## 2. Kết quả chính

| Model | Precision | Recall | F1 (test) | F1 (SUB 40) | Train (s) | Tin/s (cả lô) | p50 ms/tin | p95 ms/tin | USD / 1k tin |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **1. BoW + LogReg (tự code)** | 1.000 | 0.790 | 0.883 | 0.919 | 8.311 | 5,029.20 | 0.052 | 0.107 | 0.0 |
| **2. BoW + MLP (deep learning)** | 1.000 | 0.914 | 0.955 | 0.974 | 11.454 | 29,186.53 | 0.276 | 0.353 | 0.0 |
| **3a. Encoder (MiniLM) + kNN** | 0.876 | 0.943 | 0.908 | 0.976 | 70.580 | 30.73 | 42.020 | 53.045 | 0.0 |
| **3b. Encoder (MiniLM) + LogReg** | 0.962 | 0.971 | **0.967** | **0.976** | 70.994 | 34.73 | 26.208 | 33.931 | 0.0 |
| **3c. Encoder (MiniLM) + MLP head** | 0.971 | 0.952 | 0.962 | **0.976** | 71.453 | 34.77 | 25.485 | 33.354 | 0.0 |

## 3. Dự đoán và thực tế

Dự đoán 1: **Đoán**: F1 ~0.5, recall cao hơn precision vì dữ liệu bị lệch, các mẫu có nhãn dương chiếm phần nhiều, **Ra**: F1 ~0.88 precision cao hơn recall, **Lệch** vì hiểu sai về dữ liệu
Dự đoán 2: **Đoán**: lr=50 thì đường loss có thể sẽ đi ngang hoặc tăng lên, **Ra**: Đường loss đi mạnh xuống và đi ngang, **Lệch** vì khi lr lớn thì đồ thị loss sẽ khó đoán hơn
Dự đoán 3: **Đoán**: tương đương với mô hình linear regression. F1 sẽ giảm rõ rệt **Ra**: F1 tăng cao, **Lệch** vì dữ liệu tuyến tính

## 4. Phân tích 50 case khó


## 5. Thử thách cá nhân


## 6. Phương án cho sản phẩm thật

Với yêu cầu p95 < 50 ms/tin cho 10 triệu SMS/ngày: Chọn phương Encoder + MLP. Vì có p95, p50 thấp nhưng đánh đổi là huấn luyện lâu hơn.

## 7. AI log và điều đã học


