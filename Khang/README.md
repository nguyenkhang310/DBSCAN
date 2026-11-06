# Khang · Thuật toán DBSCAN

## Nhiệm vụ chính

Trình bày cơ sở lý thuyết DBSCAN, xây dựng thuật toán từ đầu trong notebook, thiết kế kiểm thử và đối chiếu scikit-learn. Khảo sát K-distance, chọn `eps`/`min_samples`, kiểm tra độ nhạy và bàn giao nhãn cho Khoa và Đức.

## Notebook phụ trách

[02_dbscan.ipynb](notebook/02_dbscan.ipynb) gồm **14 mục**, từ giới thiệu thuật toán đến xuất kết quả và nhận xét. Notebook hiện chỉ chứa Markdown, chưa có code, dữ liệu giả lập hoặc kết quả phân cụm.

## Đầu vào cần dùng

| Đầu vào dự kiến | Vai trò |
| --- | --- |
| `du_lieu/du_lieu_chuan_hoa/wdi_scaled.csv` | Ma trận đặc trưng sau chuẩn hóa, đi kèm khóa |
| `du_lieu/du_lieu_chuan_hoa/preprocessing_metadata.json` | Thứ tự cột, nguồn snapshot, biến đổi và phạm vi fit |
| `du_lieu/du_lieu_sach/wdi_clean.csv` | Đối chiếu khóa và diễn giải ở đơn vị gốc |

Các file trên do Đức tạo ở giai đoạn triển khai. Không tự dùng CSV gốc thay cho dữ liệu đã thống nhất mà bỏ qua tiền xử lý.

## Kết quả cần bàn giao

| Vị trí từ gốc repo | Sản phẩm dự kiến |
| --- | --- |
| `ket_qua_chung/dbscan/dbscan_labels.csv` | `country`, `year`, `cluster`, `point_type`; `-1` là noise |
| `ket_qua_chung/dbscan/tham_so_da_chon.json` | Cấu hình cuối, metric, nguồn dữ liệu, phạm vi năm và tiêu chí chọn |
| `ket_qua_chung/dbscan/grid_search.csv` | Các lần thử, tham số, số cụm, tỷ lệ nhiễu và chỉ số hợp lệ |
| `Khang/bieu_do/` | Minh họa lý thuyết, K-distance, khảo sát tham số, độ nhạy |
| `ket_qua_chung/bieu_do_bao_cao/` | Biểu đồ đã chọn cho báo cáo |

Khoa dùng nhãn để đánh giá và lập hồ sơ cụm; Đức dùng nhãn để phân tích Việt Nam. Mỗi bảng nhãn cuối phải khớp một-một với khóa dữ liệu đầu vào; các lần chạy thử được ghi riêng, không trộn vào nhãn cuối.

## Kiểm tra trước bàn giao

- Thống nhất `min_samples` bao gồm chính điểm đang xét; kiểm tra quy ước k-nearest neighbors tương ứng.
- Kiểm thử các ca biên, điểm trùng, toàn nhiễu và một cụm khi bắt đầu triển khai.
- So sánh phân hoạch theo cách không phụ thuộc số nhãn; giải thích điểm biên có nhiều cách gán hợp lệ.
- Không chọn cấu hình chỉ từ Silhouette; báo tỷ lệ nhiễu, độ phủ và độ ổn định.
- Đảm bảo nhãn, loại điểm, tập khóa và tham số xuất ra nhất quán.

Xem [quy ước kết quả](../ket_qua_chung/README.md) và [README dự án](../README.md). Chỉ phát triển code trong `.ipynb`, làm việc chung trên `main`, không tạo `.py`.
