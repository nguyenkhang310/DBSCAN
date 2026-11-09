# Khoa · Đánh giá và so sánh thuật toán

## Nhiệm vụ chính

Thiết kế đánh giá DBSCAN và so sánh với K-Means, Agglomerative Clustering, Gaussian Mixture Model. Chuẩn bị PCA 2D, hồ sơ kinh tế của từng cụm và phân tích các quan sát noise.

## Notebook phụ trách

[03_danh_gia_va_so_sanh.ipynb](notebook/03_danh_gia_va_so_sanh.ipynb) gồm **13 mục** và đã triển khai đầy đủ mã nguồn đánh giá, thuật toán đối chứng, PCA, hồ sơ cụm và phân tích noise. Notebook đang chờ hai đầu vào DBSCAN do Khang bàn giao để chạy thực nghiệm cuối trên dữ liệu thật.

## Đầu vào cần dùng

| Đầu vào dự kiến | Người bàn giao | Vai trò |
| --- | --- | --- |
| `du_lieu/du_lieu_sach/wdi_clean.csv` | Đức | Diễn giải hồ sơ cụm theo đơn vị kinh tế gốc |
| `du_lieu/du_lieu_chuan_hoa/wdi_scaled.csv` | Đức | Cùng mẫu và đặc trưng cho mọi thuật toán |
| `du_lieu/du_lieu_chuan_hoa/preprocessing_metadata.json` | Đức | Kiểm tra thứ tự biến và phạm vi tiền xử lý |
| `ket_qua_chung/dbscan/dbscan_labels.csv` | Khang | Nhãn và loại điểm DBSCAN |
| `ket_qua_chung/dbscan/tham_so_da_chon.json` | Khang | Cấu hình cuối và phạm vi mô hình |

Đường dẫn tính từ gốc repo. Khi nhận file bàn giao, giữ nguyên tên và đặt đúng đường dẫn trong bảng; không chép các file đầu vào vào `Khoa/notebook/`.

```text
DBSCAN/
├── du_lieu/
│   ├── du_lieu_sach/wdi_clean.csv
│   └── du_lieu_chuan_hoa/
│       ├── wdi_scaled.csv
│       └── preprocessing_metadata.json
└── ket_qua_chung/dbscan/
    ├── dbscan_labels.csv
    └── tham_so_da_chon.json
```

Notebook tự tìm gốc repo và hiển thị bảng `CÓ/THIẾU` cho cả năm đầu vào trước khi đọc dữ liệu. Nếu thiếu file, notebook dừng với thông báo liệt kê đúng đường dẫn cần bổ sung.

## Kết quả cần bàn giao

| Vị trí | Sản phẩm dự kiến |
| --- | --- |
| `ket_qua_chung/danh_gia/` | `so_sanh_thuat_toan.csv`, cấu hình và ghi chú về tập mẫu đánh giá |
| `ket_qua_chung/ho_so_cum/` | Thống kê đơn vị gốc, quy mô và các quan sát đại diện của từng cụm |
| `ket_qua_chung/phan_tich_nhieu/` | Danh sách noise và lý do khác biệt cần kiểm chứng |
| `Khoa/bieu_do/` | PCA 2D, so sánh thuật toán và hồ sơ cụm |
| `ket_qua_chung/bieu_do_bao_cao/` | Hình được chọn cho báo cáo |

Đức sử dụng hồ sơ cụm để phân tích Việt Nam; cả nhóm dùng bảng so sánh và nhận xét để viết báo cáo.

## Kiểm tra trước bàn giao

- Ghép bảng bằng `country` + `year` và kiểm tra một-một; không dựa vào vị trí dòng.
- Giữ cùng đặc trưng, chuẩn hóa và mẫu đầu vào giữa các thuật toán.
- Báo chính sách noise, `n_evaluated`, `coverage` và số cụm đi kèm mỗi chỉ số.
- Chỉ tính chỉ số khi `2 ≤ số nhãn < số mẫu`; dùng `N/A` kèm lý do nếu không hợp lệ.
- So sánh thêm trên cùng tập con non-noise của DBSCAN, giữ nhãn đã fit trên toàn mẫu và ghi rõ phạm vi.
- Dùng PCA để trực quan hóa, báo tỷ lệ phương sai giải thích; diễn giải đặc trưng bằng dữ liệu đơn vị gốc.
- Không kết luận noise tương đương khủng hoảng kinh tế khi chưa có bằng chứng bổ sung.

Xem [quy ước kết quả](../ket_qua_chung/README.md) và [README dự án](../README.md). Toàn bộ code nằm trong `.ipynb`; dùng chung `main`, không tạo `.py`.
