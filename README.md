# ⌚ Phân Tích Phân Khúc Giá Đồng Hồ

## 👥 Tác Giả

**KHDL 22.13 - Nhóm 10**

-   Trương Vũ Linh
-   Hoàng Văn Đạt
-   Đỗ Văn Tuấn

---

## 📊 Đề Bài

Phân cụm và phân loại phân khúc giá của đồng hồ theo các thông số kỹ thuật, thương hiệu, màu sắc và các đặc tính khác.

---

## 📁 Cấu Trúc Thư Mục

-   **notebooks/**

    -   `craw_data.ipynb`: Mã thu thập dữ liệu bằng web scraping
    -   `clean_data.ipynb`: Làm sạch và tiền xử lý dữ liệu
    -   `train_test_split.ipynb`: Chia tập dữ liệu thành tập huấn luyện và kiểm tra
    -   `clustering.ipynb`: Phân tích phân cụm giá đồng hồ
    -   `classification.ipynb`: Mô hình phân loại phân khúc giá đồng hồ

-   **data/**

    -   `product_cleaned.csv`: Dữ liệu đã làm sạch trước khi phân đoạn

-   **dataset/**
    -   `train_segmented.csv`: Tập dữ liệu huấn luyện với phân khúc giá (5665 mẫu, 15 cột)
    -   `test_segmented.csv`: Tập dữ liệu kiểm tra với phân khúc giá (1476 mẫu, 15 cột)

---

## 🔄 Quy Trình Xử Lý Dữ Liệu

1. **Thu Thập Dữ Liệu**: 🕸️ Thu thập thông tin đồng hồ bằng web scraping
2. **Làm Sạch Dữ Liệu**: 🧹 Tiền xử lý và làm sạch dữ liệu thô
3. **Kỹ Thuật Đặc Trưng**: 🔧 Mã hóa các biến phân loại
4. **Chia Tập Dữ Liệu**: ✂️ Tạo tập dữ liệu huấn luyện và kiểm tra
5. **Phân Tích**: 🔍 Phân cụm và phân loại phân khúc giá

---

## 🛠️ Kỹ Thuật Đặc Trưng

-   **Mã Hóa Mục Tiêu (Target Encoding)**:

    -   Chất liệu vỏ (Case Material)
    -   Chất liệu dây đeo (Band Material)
    -   Mặt sau vỏ (Case Back)
    -   Chất liệu vành (Bezel Material)
    -   Thương hiệu (Brand)

-   **Mã Hóa One-hot + Mã Hóa Mục Tiêu**:

    -   Giới tính (Gender)
    -   Bộ máy (Movement)

-   **Chỉ Mã Hóa Mục Tiêu**:
    -   Mặt kính (Crystal)
    -   Kim đồng hồ (Hands)
    -   Đánh dấu mặt số (Dial Marker)

---

## 💰 Phân Khúc Giá

Cột giá đã được chuyển đổi thành phân khúc giá (0-4) trong cả hai tập dữ liệu:

| Phân khúc | Danh mục               | Khoảng giá (₫)  | Số lượng train | Tỉ lệ train | Số lượng test | Tỉ lệ test |
| --------- | ---------------------- | --------------- | -------------- | ----------- | ------------- | ---------- |
| 0         | Giá rẻ (Budget)        | < 1.000         | 2456           | 43,35%      | 656           | 44,44%     |
| 1         | Phổ thông (Affordable) | 1.000 - 9.999   | 1796           | 31,70%      | 458           | 31,03%     |
| 2         | Trung cấp (Mid-Range)  | 10.000 - 29.999 | 773            | 13,65%      | 188           | 12,74%     |
| 3         | Cao cấp (Premium)      | 30.000 - 99.999 | 480            | 8,47%       | 136           | 9,21%      |
| 4         | Siêu cao cấp (Luxury)  | ≥ 100.000       | 160            | 2,82%       | 38            | 2,57%      |

---

## 📈 Bài Toán Phân Tích

Hai bài toán phân tích chính sẽ được thực hiện trên tập dữ liệu này:

1. **Phân Cụm**: 🔠 Học không giám sát để khám phá các nhóm tự nhiên trong dữ liệu đồng hồ
2. **Phân Loại**: 🏷️ Học có giám sát để dự đoán phân khúc giá dựa trên các đặc tính của đồng hồ
