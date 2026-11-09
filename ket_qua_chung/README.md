# Kết quả chung

| Thư mục | Người phụ trách | Sản phẩm |
| --- | --- | --- |
| `dbscan/` | Khang | Nhãn, tham số, Grid Search, độ nhạy/ổn định |
| `danh_gia/` | Khoa | So sánh chỉ số và mô hình đối chứng |
| `ho_so_cum/` | Khoa | Thống kê đơn vị gốc và quan sát đại diện |
| `phan_tich_nhieu/` | Khoa | Noise và ba đặc trưng lệch nhiều nhất |
| `viet_nam/` | Đức | Việt Nam, Đông Nam Á và đối chiếu bản đồ |
| `bieu_do_bao_cao/` | Cả nhóm | Hình đã chọn |

`dbscan_labels.csv` có bốn cột `country, year, cluster, point_type`. Khóa country–year duy nhất; -1 tương ứng noise. Nhãn fit toàn panel, không trộn các lần chạy.

`tham_so_da_chon.json` ghi tham số, thứ tự biến, checksum, phạm vi fit và kiểm thử. `quality_target_met=false` nghĩa là chưa đạt độ phủ mong muốn.

So sánh chỉ số trên đúng cùng tập mẫu. Noise không phải một cụm kinh tế; chỉ số không hợp lệ ghi thiếu, không thay bằng 0. [Biên bản kiểm thử](../bao_cao/KIEM_THU_TOAN_BO.md).
