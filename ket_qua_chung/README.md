# Kết quả chung

| Thư mục | Người phụ trách | Sản phẩm |
| --- | --- | --- |
| `dbscan/` | Khang | Nhãn toàn panel, Grid Search, độ nhạy và thí nghiệm ngoài mẫu |
| `danh_gia/` | Khoa | So sánh chỉ số và mô hình đối chứng |
| `ho_so_cum/` | Khoa | Thống kê đơn vị gốc và quan sát đại diện |
| `phan_tich_nhieu/` | Khoa | Noise và ba đặc trưng lệch nhiều nhất |
| `viet_nam/` | Đức | Việt Nam, Đông Nam Á và đối chiếu bản đồ |

`dbscan_labels.csv` có bốn cột `country, year, cluster, point_type`. Khóa country–year duy nhất; -1 tương ứng noise. Nhãn fit toàn panel, không trộn các lần chạy.

`tham_so_da_chon.json` ghi tham số, thứ tự biến, checksum, phạm vi fit và kiểm thử. `quality_target_met=false` nghĩa là chưa đạt độ phủ mong muốn.

So sánh chỉ số trên đúng cùng tập mẫu. Noise không phải một cụm kinh tế; chỉ số không hợp lệ ghi thiếu, không thay bằng 0. [Biên bản kiểm thử](../bao_cao/KIEM_THU_TOAN_BO.md).

Các file có `ngoai_mau` và `chia_tap_theo_quoc_gia.csv` thuộc thí nghiệm chia quốc gia 60%/20%/20%; không dùng để thay nhãn toàn panel. Tham số chuẩn hóa trong `cau_hinh_ngoai_mau.json` chỉ fit train. Hình báo cáo liên kết trực tiếp từ thư mục mỗi thành viên.
