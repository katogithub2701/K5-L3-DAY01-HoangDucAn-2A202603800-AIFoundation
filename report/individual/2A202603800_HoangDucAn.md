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

| Mô hình | Precision | Recall | F1 (test) | F1 (SUB 40) | Train (s) | Tin/s (cả lô) | p50 ms/tin | p95 ms/tin | USD / 1k tin |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **1. BoW + LogReg (tự code)** | 1.000 | 0.790 | 0.883 | 0.919 | 4.127 | 26167.826 | 0.046 | 0.067 | 0.0 |
| **2. BoW + MLP (deep learning)** | 1.000 | 0.914 | 0.955 | 0.974 | 4.262 | 44929.383 | 0.163 | 0.202 | 0.0 |
| **3a. Encoder (MiniLM) + kNN** | 0.876 | 0.943 | 0.908 | 0.976 | 82.931 | 28.040 | 47.237 | 71.138 | 0.0 |
| **3b. Encoder (MiniLM) + LogReg** | 0.962 | 0.971 | 0.967 | 0.976 | 85.060 | 32.839 | 30.344 | 49.163 | 0.0 |
| **3c. Encoder (MiniLM) + MLP head** | 0.971 | 0.952 | 0.962 | 0.976 | 84.242 | 29.824 | 45.015 | 70.083 | 0.0 |

## 3. Dự đoán và thực tế

Dự đoán 1: **Đoán**: F1 ~0.5, recall cao hơn precision vì dữ liệu bị lệch, các mẫu có nhãn dương chiếm phần nhiều, **Ra**: F1 ~0.88 precision cao hơn recall, **Lệch** vì hiểu sai về dữ liệu

Dự đoán 2: **Đoán**: lr=50 thì đường loss có thể sẽ đi ngang hoặc tăng lên, **Ra**: Đường loss đi mạnh xuống và đi ngang, **Lệch** vì khi lr lớn thì đồ thị loss sẽ khó đoán hơn

Dự đoán 3: **Đoán**: tương đương với mô hình linear regression. F1 sẽ giảm rõ rệt **Ra**: F1 tăng cao, **Lệch** vì dữ liệu tuyến tính

## 4. Phân tích 50 case khó

Mô hình BoW + LogReg giảm nhiều nhất. Với case Tháo túng/lừa đảo: Do đặc trưng từ BoW không thể hiện được ý nghĩa của ngữ cảnh, mối liên hệ giữa các từ. Với case Spam giọng tự nhiên: Do đặc trưng từ BoW chỉ thể hiện sự xuất hiện của từ trong câu, không mang ý nghĩa ngữ cảnh

## 5. Thử thách cá nhân

Thay đổi max_tokens trong hàm build_vocab và train lại mô hình:

Kết quả: Với vocab = 100, F1_test = 0.085; Với vocab = 5000, F1_test = 0.883.

Giải thích: Từ điển có quá ít từ sẽ khiến mô hình có ít thông tin với các từ quan trọng để phân loại nhãn, từ đó khó phân loại chính xác hơn.

## 6. Phương án cho sản phẩm thật

Cách Encoder + LogReg đạt cả độ trễ và chất lượng. Ước tính khoảng 3700$ 1 tháng nếu dùng mỗi 1M Token = 0.15$ nếu sử dụng LLM

## 7. AI log và điều đã học

Câu 1 - Hỏi: Đối với reasoning model, nếu đặt max_tokens = 3 sẽ như thế nào, Nhận: Quy trình suy luận bị ngắt, không in ra kết quả

Câu 2 - Hỏi: Gửi đoạn mã lỗi và giải thích, Nhận: Giải thích về mã lỗi

Học được: Mô hình lớn hơn, phức tạp hơn chưa chắc có kết quả tốt nhất, cần phải dựa vào các yếu tố như độ phức tạp bài toán, độ trễ, độ chính xác,...
