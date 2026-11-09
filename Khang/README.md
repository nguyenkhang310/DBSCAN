# Nguyên Khang · DBSCAN

[Notebook 02](notebook/02_dbscan.ipynb) gồm 14 mục: cơ sở lý thuyết, DBSCAN tự viết, kiểm thử, K-distance, Grid Search, đánh giá độ nhạy và kiểm định ngoài mẫu.

## Hai mô hình

Mô hình **toàn panel** dùng dữ liệu chuẩn hóa của Đức và tạo nhãn cho các notebook 03–04: eps=0,865, min_samples=24, bốn cụm, độ phủ 32,79%, Silhouette non-noise 0,1889.

Thí nghiệm **ngoài mẫu** chia 162 quốc gia thành 97 train, 32 validation, 33 test, seed 42. RobustScaler chỉ fit train; validation chọn eps=0,902, min_samples=16. Điểm mới nhận nhãn core train gần nhất trong eps hoặc bị từ chối. Test phủ 19,82% và chỉ có một nhãn được gán, nên ba chỉ số nội bộ là N/A. Không gộp nhãn thí nghiệm này vào nhãn toàn panel.

## Kết quả lưu ở ket_qua_chung/dbscan/

| File | Vai trò |
| --- | --- |
| `dbscan_labels.csv`, `tham_so_da_chon.json` | Nhãn toàn panel, cấu hình và checksum |
| `grid_search.csv` | 90 cấu hình mô tả toàn panel |
| `doi_chieu_sklearn.csv` | 36 cấu hình giả lập đối chiếu |
| `do_nhay.csv`, `do_on_dinh.csv` | Tham số, thứ tự, nhiễu nhỏ và lấy mẫu theo quốc gia |
| `kiem_tra_thang_do.csv`, `kiem_tra_tung_nam.csv` | Chẩn đoán thang đo và mật độ theo năm |
| `quy_mo_cum.csv` | Số điểm và quốc gia mỗi cụm/noise |
| `chia_tap_theo_quoc_gia.csv` | Tập train/validation/test của từng khóa |
| `grid_search_ngoai_mau.csv` | Kết quả train và validation, không dùng test |
| `danh_gia_ngoai_mau.csv`, `nhan_ngoai_mau.csv` | Chỉ số và nhãn của từng tập |
| `cau_hinh_ngoai_mau.json` | Phép chia, scaler train, quy tắc gán và cấu hình lựa chọn |

Hàm DBSCAN tự viết dùng NumPy và hàng đợi; các hàm còn lại dùng để kiểm thử, thống kê và gán điểm ngoài mẫu. Tất cả đều được gọi trong notebook. Biểu đồ lưu tại [bieu_do/](bieu_do/).

[Quy trình](../README.md) · [Báo cáo](../bao_cao/BAO_CAO_KET_QUA.md) · [Kiểm thử](../bao_cao/KIEM_THU_TOAN_BO.md).
