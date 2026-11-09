# Dữ liệu

## File sử dụng

| File | Nội dung |
| --- | --- |
| [wdi_2010_2024.csv](du_lieu_tho/wdi_2010_2024.csv) | Gốc dạng rộng: 3.990 hàng × 12 cột |
| [wdi_2010_2024_long.csv](du_lieu_tho/wdi_2010_2024_long.csv) | Gốc dạng dài: 31.920 giá trị chỉ tiêu |
| [manifest.json](du_lieu_tho/manifest.json), [SHA256SUMS](du_lieu_tho/SHA256SUMS) | Nguồn, URL, ngày tải và checksum 19 file |
| [nguon_api/](du_lieu_tho/nguon_api/) | 17 phản hồi API gốc |
| [tu_dien_chi_tieu.csv](tu_dien_chi_tieu.csv) | Mã, tên và đơn vị 8 biến |
| [wdi_clean.csv](du_lieu_sach/wdi_clean.csv) | 2315 quốc gia–năm, 162 nền kinh tế, đơn vị gốc |
| [nhat_ky_noi_suy.csv](du_lieu_sach/nhat_ky_noi_suy.csv) | 32 ô được điền |
| [wdi_scaled.csv](du_lieu_chuan_hoa/wdi_scaled.csv) | Cùng khóa, 8 biến chuẩn hóa |
| [preprocessing_metadata.json](du_lieu_chuan_hoa/preprocessing_metadata.json) | Quy tắc xử lý, tham số và checksum đầu ra |

## Quy tắc

Nguồn WDI gồm 217 nền kinh tế và 49 nhóm tổng hợp, giai đoạn 2010–2024. Bảng rộng dùng khóa `country, year`; bảng dài thêm `indicator`. Ô trống là thiếu dữ liệu, không phải số 0. `country` là mã ba ký tự World Bank, thường tương ứng ISO3.

Dữ liệu sạch loại `is_aggregate=1`. Nội suy tuyến tính chỉ cho toàn khoảng thiếu bên trong dài tối đa 2 năm; điền biên chỉ khi toàn khoảng biên dài 1 năm. Khoảng dài giữ thiếu, rồi bỏ hàng chưa đủ 8 biến. Giữ giá trị cực trị, ghi mọi ô được điền vào nhật ký, kể cả hàng sau đó vẫn bị loại vì thiếu biến khác.

Trước RobustScaler, dùng log1p cho GDP/người, thất nghiệp, thương mại/GDP và chi tiêu chính phủ/GDP; signed-log1p cho lạm phát. Ba biến còn lại giữ thang tuyến tính. Fit toàn panel để mô tả hồi cứu. Không đưa mã, tên quốc gia, năm hoặc cờ nhóm tổng hợp vào khoảng cách.

CSV/JSON/Notebook dùng LF theo `.gitattributes`; checksum của đầu ra được tính lại khi chạy notebook 01. Không sửa dữ liệu thô khi chạy các notebook.

## Nguồn và bản đồ

[World Bank WDI](https://datacatalog.worldbank.org/search/dataset/0037712/world-development-indicators), source 2, snapshot 07/11/2026, [CC BY 4.0](https://datacatalog.worldbank.org/public-licenses#cc-by). Metadata gốc giữ tên tổ chức cung cấp từng chỉ tiêu.

Bản CSV gốc gắn mã quốc gia qua `country.id` → metadata `iso2Code` → `id`, tránh gộp 5 nhóm tổng hợp có `countryiso3code` trống. Chỉ đổi định dạng, không làm sạch dữ liệu ở snapshot gốc.

[Bản đồ Natural Earth](ban_do/README.md) lưu sẵn cho notebook 04; dùng mã ADM0_A3. Quốc gia thiếu hình học được xuất riêng, không xem là noise hoặc thiếu dữ liệu kinh tế.
