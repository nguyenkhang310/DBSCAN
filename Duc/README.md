# Đức · Dữ liệu và phân tích ứng dụng

## Nhiệm vụ chính

Chuẩn bị dữ liệu WDI cho cả nhóm: kiểm tra nguồn, dữ liệu thiếu/trùng, loại nhóm tổng hợp, EDA, tương quan, biến đổi và chuẩn hóa. Sau khi Khang và Khoa bàn giao kết quả, phân tích Việt Nam, so sánh Đông Nam Á và xây dựng bản đồ phân cụm.

## Notebook phụ trách

| Notebook | Thời điểm thực hiện | Phạm vi |
| --- | --- | --- |
| [01_tien_xu_ly_du_lieu.ipynb](notebook/01_tien_xu_ly_du_lieu.ipynb) | Đầu quy trình | 10 mục từ kiểm tra nguồn tới bàn giao dữ liệu |
| [04_phan_tich_viet_nam.ipynb](notebook/04_phan_tich_viet_nam.ipynb) | Sau notebook 02 và 03 | 6 mục về Việt Nam, Đông Nam Á và bản đồ |

Cả hai notebook đang là **khung Markdown**, chưa có code hoặc kết quả thực nghiệm.

## Đầu vào

- Bắt đầu từ [CSV WDI gốc](../du_lieu/du_lieu_tho/wdi_2010_2024.csv), [từ điển chỉ tiêu](../du_lieu/tu_dien_chi_tieu.csv), JSON nguồn và manifest/checksum trong `du_lieu/du_lieu_tho/`.
- Notebook 04 sẽ dùng dữ liệu sạch, `ket_qua_chung/dbscan/dbscan_labels.csv`, `tham_so_da_chon.json` và hồ sơ cụm do Khoa lập. Đây là các sản phẩm dự kiến, chưa có sẵn.

## Kết quả cần bàn giao

| Nơi lưu | Sản phẩm dự kiến | Người nhận |
| --- | --- | --- |
| `du_lieu/du_lieu_sach/` | `wdi_clean.csv` ở đơn vị gốc | Khang, Khoa và notebook 04 |
| `du_lieu/du_lieu_chuan_hoa/` | `wdi_scaled.csv`, `preprocessing_metadata.json` | Khang và Khoa |
| `Duc/bieu_do/` | EDA, tương quan, diễn biến Việt Nam, so sánh khu vực, bản đồ | Cả nhóm |
| `ket_qua_chung/bieu_do_bao_cao/` | Biểu đồ đã chọn cho báo cáo, kèm chú thích/nguồn | Cả nhóm |

Đường dẫn trong bảng tính từ gốc repo. Không lưu đè dữ liệu gốc; không tạo file đầu ra giả ở bước khởi tạo.

## Kiểm tra trước bàn giao

- Chốt phân cụm từng năm hay gộp nhiều năm; ghi rõ cách chọn mẫu và phạm vi fit chuẩn hóa.
- Loại nhóm tổng hợp bằng `is_aggregate`/metadata, không dùng độ dài mã quốc gia để lọc.
- Dùng khóa `country` + `year`, kiểm tra duy nhất và khớp giữa dữ liệu sạch/chuẩn hóa.
- Không đưa mã quốc gia, tên, năm hoặc `is_aggregate` vào ma trận đặc trưng mặc định.
- Lưu thứ tự `feature_columns`, xử lý thiếu, biến đổi và tham số chuẩn hóa trong metadata.
- So sánh nhãn qua năm dựa trên hồ sơ/thành viên cụm nếu mỗi năm được fit riêng.

Xem [hợp đồng dữ liệu](../du_lieu/README.md), [quy ước kết quả](../ket_qua_chung/README.md) và [cách làm việc chung trên main](../README.md#làm-việc-nhóm-trên-main). Toàn bộ code triển khai sau này nằm trong notebook, không tạo `.py`.
