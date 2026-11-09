# Đức

- [01 · Tiền xử lý](notebook/01_tien_xu_ly_du_lieu.ipynb): kiểm tra nguồn, loại nhóm tổng hợp, nội suy ngắn, EDA, tương quan và chuẩn hóa.
- [04 · Việt Nam](notebook/04_phan_tich_viet_nam.ipynb): vị trí qua năm, Đông Nam Á và bản đồ ngoại tuyến.

Chạy 01 trước Khang/Khoa; chạy 04 sau 03. Đầu vào ở `du_lieu/du_lieu_tho/`. Dữ liệu sạch/chuẩn hóa và nhật ký nội suy lưu trong `du_lieu/`; kết quả ứng dụng ở `ket_qua_chung/viet_nam/`, biểu đồ tại `Duc/bieu_do/`.

Nội suy chỉ lấp toàn khoảng thiếu bên trong dài tối đa 2 năm hoặc toàn khoảng biên dài 1 năm. Không xóa ngoại lệ theo IQR. Mỗi bước dùng khóa country–year.

[Xem quy trình và kiểm thử](../README.md).
