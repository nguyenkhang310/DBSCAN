# Khoa

[03_danh_gia_va_so_sanh.ipynb](notebook/03_danh_gia_va_so_sanh.ipynb) gồm 13 mục đánh giá DBSCAN, K-Means, Agglomerative và GMM; PCA, hồ sơ cụm và phân tích noise.

Chạy sau 02. Đầu vào gồm dữ liệu sạch/chuẩn hóa, metadata, nhãn và tham số DBSCAN. Chọn k=2..10; K-Means/Agglomerative theo Silhouette, GMM theo BIC và phải hội tụ.

Bảng so sánh có hai phạm vi: chính sách từng thuật toán và cùng tập non-noise của DBSCAN. Giữ nguyên nhãn đã fit khi đánh giá tập con; chỉ số không hợp lệ ghi thiếu kèm lý do.

Kết quả ở `ket_qua_chung/danh_gia/`, `ho_so_cum/`, `phan_tich_nhieu/`; 4 biểu đồ ở `Khoa/bieu_do/`.

[Quy trình chạy](../README.md) · [Kiểm thử](../bao_cao/KIEM_THU_TOAN_BO.md).

Bảng đánh giá dùng mô hình toàn panel; kết quả train/validation/test là thí nghiệm riêng trong notebook 02. Không báo accuracy khi không có nhãn chuẩn. Hồ sơ cụm chỉ lưu một bảng dạng dài, tránh xuất lặp.

[Báo cáo kết quả](../bao_cao/BAO_CAO_KET_QUA.md).
