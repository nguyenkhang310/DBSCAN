# Nguyên Khang

[02_dbscan.ipynb](notebook/02_dbscan.ipynb) gồm đủ 14 mục: lý thuyết, DBSCAN tự viết, kiểm thử, K-distance, Grid Search, độ nhạy và bàn giao.

Chạy sau 01. Đọc dữ liệu sạch, chuẩn hóa và metadata của Đức. Xuất 8 CSV và 1 JSON trong `ket_qua_chung/dbscan/`; 5 biểu đồ ở `Khang/bieu_do/`.

Hàm DBSCAN chính 40 dòng, dùng NumPy và hàng đợi. Có 8 ca biết đáp án, 11 ca đầu vào sai, 36 cấu hình giả lập đối chiếu scikit-learn, kiểm tra border và đối chiếu toàn bộ WDI.

Hiện có 4 cụm, noise 67.21%, Silhouette non-noise 0.1889. Chưa đạt mục tiêu độ phủ; không gọi đây là mô hình phân cụm tốt.

[Quy trình chạy](../README.md) · [Kiểm thử](../bao_cao/KIEM_THU_TOAN_BO.md).
