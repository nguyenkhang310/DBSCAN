# DBSCAN · Economics

![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)

Phân cụm quốc gia theo đặc điểm kinh tế vĩ mô, phát hiện quan sát khác biệt và phân tích Việt Nam. Dữ liệu World Bank WDI, 8 chỉ tiêu, giai đoạn 2010–2024.

## Quy trình và phân công

| Thứ tự | Thành viên | Notebook |
| --- | --- | --- |
| 01 | Đức | [Tiền xử lý dữ liệu](Duc/notebook/01_tien_xu_ly_du_lieu.ipynb) |
| 02 | Nguyên Khang | [DBSCAN từ đầu và kiểm thử](Khang/notebook/02_dbscan.ipynb) |
| 03 | Khoa | [Đánh giá và so sánh](Khoa/notebook/03_danh_gia_va_so_sanh.ipynb) |
| 04 | Đức | [Việt Nam, Đông Nam Á và bản đồ](Duc/notebook/04_phan_tich_viet_nam.ipynb) |

Chạy theo thứ tự **01 → 02 → 03 → 04**. Toàn bộ code nằm trong notebook, không có file `.py`.

## Cài đặt và chạy

Dùng Python 3.12:

```bash
git clone https://github.com/nguyenkhang310/DBSCAN.git
cd DBSCAN
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter notebook
```

Windows: tạo môi trường bằng `py -3.12 -m venv .venv`, kích hoạt bằng `.\.venv\Scripts\Activate.ps1`.

Trong Jupyter hoặc VS Code, chọn kernel `.venv`, mở từng notebook và **Restart Kernel → Run All**. Có thể mở từ gốc repo hoặc thư mục notebook. Dữ liệu và bản đồ đã lưu sẵn; chạy không cần Internet sau khi cài thư viện.

## Dữ liệu và bàn giao

- [CSV gốc](du_lieu/du_lieu_tho/wdi_2010_2024.csv): 3.990 hàng, gồm 217 nền kinh tế và 49 nhóm tổng hợp.
- [CSV sạch](du_lieu/du_lieu_sach/wdi_clean.csv): **2,315 quốc gia–năm, 162 nền kinh tế** sau lọc và nội suy ngắn hạn.
- [CSV chuẩn hóa](du_lieu/du_lieu_chuan_hoa/wdi_scaled.csv): 8 biến, log/signed-log và RobustScaler toàn panel.
- [Metadata](du_lieu/du_lieu_chuan_hoa/preprocessing_metadata.json) ghi thứ tự biến, tham số và checksum; [nhật ký nội suy](du_lieu/du_lieu_sach/nhat_ky_noi_suy.csv) ghi các ô được điền.

Khóa bàn giao là **`country` + `year`**, mỗi khóa một hàng. Mô hình dùng quốc gia–năm; mã quốc gia/năm không tham gia khoảng cách. Tất cả lần chạy dùng chung hệ cụm panel.

## Cấu trúc repository

| Nơi lưu | Nội dung |
| --- | --- |
| `du_lieu/` | Dữ liệu gốc, sạch, chuẩn hóa, ranh giới bản đồ |
| `Duc/`, `Khang/`, `Khoa/` | Notebook và biểu đồ từng người |
| `ket_qua_chung/dbscan/` | Nhãn, tham số, Grid Search, độ nhạy |
| `ket_qua_chung/danh_gia/` | Chỉ số và thuật toán đối chứng |
| `ket_qua_chung/ho_so_cum/`, `phan_tich_nhieu/` | Hồ sơ cụm và noise |
| `ket_qua_chung/viet_nam/` | Việt Nam, Đông Nam Á, kiểm tra bản đồ |
| `ket_qua_chung/bieu_do_bao_cao/` | Hình dùng chung |
| `bao_cao/` | Biên bản kiểm thử và thư mục slide |

## Kết quả và giới hạn

DBSCAN chọn `eps=0.865`, `min_samples=24`: **4 cụm**, 759 điểm thuộc cụm, **noise 67.21%**, Silhouette non-noise **0.1889**. Bản tự viết khớp scikit-learn về phân hoạch, core và noise.

Cấu hình chưa đạt độ phủ 65% trong lưới 90 lần thử, chỉ dùng thăm dò. Không xem noise là bằng chứng khủng hoảng. Điểm số phải đọc cùng độ phủ; Khoa có bảng so sánh trên cùng tập non-noise để tránh so các mẫu khác nhau. Nội suy và chuẩn hóa toàn panel phục vụ hồi cứu, không đánh giá dự báo.

[Kiểm thử toàn bộ](bao_cao/KIEM_THU_TOAN_BO.md) · [Hướng dẫn dữ liệu](du_lieu/README.md) · [Đức](Duc/README.md) · [Khang](Khang/README.md) · [Khoa](Khoa/README.md)

## Làm việc nhóm

Dùng chung `main`. Cập nhật trước khi sửa, kiểm tra diff và chạy notebook trước khi commit. Không force push, không commit `.venv`, checkpoint hoặc thông tin đăng nhập. `.gitattributes` giữ CSV/JSON/Notebook dùng LF để checksum nhất quán.

## Nguồn

[World Bank WDI](https://datacatalog.worldbank.org/search/dataset/0037712/world-development-indicators), [CC BY 4.0](https://datacatalog.worldbank.org/public-licenses#cc-by), snapshot 07/11/2026. [Natural Earth](du_lieu/ban_do/README.md) cung cấp ranh giới bản đồ public domain. [scikit-learn](https://scikit-learn.org/stable/modules/clustering.html#dbscan) là nguồn đối chiếu thuật toán.
