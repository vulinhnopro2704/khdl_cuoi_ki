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

    -   `link.csv`: Danh sách các liên kết sản phẩm đồng hồ thu thập được
    -   `raw_data.csv`: Dữ liệu thô thu thập từ web scraping (có thể chứa lỗi và thiếu sót)
    -   `data_cleaned.csv`: Dữ liệu đã làm sạch trước khi chia dữ liệu

-   **dataset/**
    -   `encoding_params.json`: Tham số mã hóa cho các đặc trưng phân loại
    -   `predicted_segments.csv`: Kết quả dự đoán phân khúc giá từ mô hình
    -   `raw_data_train.csv`: Tập dữ liệu huấn luyện với phân khúc giá (5665 mẫu, 15 cột) chưa phân loại
    -   `raw_data_test.csv`: Tập dữ liệu kiểm tra với phân khúc giá (1476 mẫu, 15 cột) chưa phân loại
    -   `cleaned_data_train.csv`: Tập dữ liệu huấn luyện với phân khúc giá (5665 mẫu, 15 cột) phân loại phân khúc giá
    -   `cleaned_data_test.csv`: Tập dữ liệu kiểm tra với phân khúc giá (1476 mẫu, 15 cột) phân loại phân khúc giá

---

## 🔄 Quy Trình Xử Lý Dữ Liệu

1. **Thu Thập Dữ Liệu**: 🕸️ Thu thập thông tin đồng hồ bằng web scraping
2. **Làm Sạch Dữ Liệu**: 🧹 Tiền xử lý và làm sạch dữ liệu thô
3. **Chia Tập Dữ Liệu**: ✂️ Tạo tập dữ liệu huấn luyện và kiểm tra
4. **Phân Tích**: 🔍 Phân cụm và phân loại phân khúc giá

---

## 🛠️ Kỹ Thuật Đặc Trưng

**Smoothing Encoding**

-   **Mã Hóa Mục Tiêu (Target Encoding)**:

    -   Chất liệu vỏ (Case Material)
    -   Chất liệu dây đeo (Band Material)
    -   Mặt sau vỏ (Case Back)
    -   Chất liệu vành (Bezel Material)
    -   Thương hiệu (Brand)
    -   Kiểu đồng hồ (Watch Style)

-   **Mã Hóa One-hot**:

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

Hai bài toán phân tích chính đã được thực hiện trên tập dữ liệu này:

### 1. Phân Cụm 🔠

Học không giám sát để khám phá các nhóm tự nhiên trong dữ liệu đồng hồ.

### 2. Phân Loại 🏷️

Học có giám sát để dự đoán phân khúc giá dựa trên các đặc tính của đồng hồ.

#### Các mô hình đã thử nghiệm:

- **K-Nearest Neighbors (KNN)**: Đạt độ chính xác 79.8% với k=9
- **Random Forest (RF)**: Đạt độ chính xác 89.7% với tham số tối ưu (max_depth=30, n_estimators=253)

#### Đánh giá mô hình trên tập kiểm tra:

| Phân khúc             | Độ chính xác | Độ chính xác (%) |
|-----------------------|--------------|-----------------|
| Giá rẻ (Budget)       | 632/656      | 96.34%          |
| Phổ thông (Affordable)| 426/458      | 93.01%          |
| Trung cấp (Mid-Range) | 143/188      | 76.06%          |
| Cao cấp (Premium)     | 101/136      | 74.26%          |
| Siêu cao cấp (Luxury) | 22/38        | 57.89%          |
| **Tổng hợp**          | **1324/1476**| **89.70%**      |

#### Đặc trưng quan trọng:

Thương hiệu (brand), chất liệu vành (bezel_material) và mặt kính (crystal) là các đặc trưng quan trọng nhất trong việc xác định phân khúc giá của đồng hồ.

---

## 🔍 Kết Luận

- Mô hình Random Forest cho kết quả tốt nhất với độ chính xác 89.70% trên tập kiểm tra.
- Phân khúc giá rẻ và phổ thông dễ phân loại nhất với độ chính xác trên 93%.
- Phân khúc siêu cao cấp khó phân loại nhất, có thể do số lượng mẫu ít hoặc đặc điểm phức tạp.
- Các đặc trưng liên quan đến thương hiệu và chất liệu có ảnh hưởng lớn nhất đến giá.

Kết quả này có thể được ứng dụng để:
- Tự động phân loại đồng hồ mới vào các phân khúc giá
- Hỗ trợ doanh nghiệp định vị sản phẩm trong thị trường
- Đưa ra chiến lược giá phù hợp dựa trên các đặc tính sản phẩm
