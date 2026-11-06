# Dữ liệu · World Bank WDI

## Mở file nào?

**Dùng [du_lieu_tho/wdi_2010_2024.csv](du_lieu_tho/wdi_2010_2024.csv) làm điểm bắt đầu cho notebook 01.** Đây là bảng rộng, có thể đọc trực tiếp bằng pandas ở giai đoạn triển khai. Dữ liệu đã nằm trong repo nên có thể làm việc ngoại tuyến sau khi clone.

| File / thư mục | Nội dung | Trạng thái |
| --- | --- | --- |
| [wdi_2010_2024.csv](du_lieu_tho/wdi_2010_2024.csv) | 3.990 thực thể–năm, 12 cột, 8 chỉ tiêu | Có sẵn, giữ cả nhóm tổng hợp |
| [wdi_2010_2024_long.csv](du_lieu_tho/wdi_2010_2024_long.csv) | 31.920 thực thể–năm–chỉ tiêu, 7 cột | Có sẵn, cùng giá trị với bảng rộng |
| [nguon_api/](du_lieu_tho/nguon_api/) | 8 phản hồi dữ liệu JSON, metadata quốc gia và 8 metadata chỉ tiêu | Nguyên byte phản hồi World Bank |
| [manifest.json](du_lieu_tho/manifest.json) | URL, thời điểm tải, phiên bản nguồn, số bản ghi, quy tắc xuất CSV và SHA-256 | Có sẵn |
| [SHA256SUMS](du_lieu_tho/SHA256SUMS) | Checksum của 19 file dữ liệu/metadata | Có sẵn |
| [tu_dien_chi_tieu.csv](tu_dien_chi_tieu.csv) | Mã cột, tên và đơn vị của 8 chỉ tiêu | Có sẵn |
| [du_lieu_sach/](du_lieu_sach/) | `wdi_clean.csv` do Đức bàn giao | Chưa tạo dữ liệu, chỉ có `.gitkeep` |
| [du_lieu_chuan_hoa/](du_lieu_chuan_hoa/) | `wdi_scaled.csv`, `preprocessing_metadata.json` | Chưa tạo dữ liệu, chỉ có `.gitkeep` |

## Phạm vi snapshot

- **Nguồn:** World Development Indicators, API source `2` của World Bank.
- **Thời gian:** 2010–2024, 15 năm; truy cập ngày **07/11/2026**.
- **Phiên bản WDI:** trường `lastupdated` của 8 phản hồi dữ liệu là `2026-10-08`.
- **Thực thể:** 266, gồm 217 quốc gia/vùng lãnh thổ và 49 nhóm tổng hợp vùng/thu nhập.
- **Giá trị:** 31.920 quan sát chỉ tiêu, trong đó 3.354 giá trị `null` được xuất thành ô CSV trống.
- **Việt Nam:** `VNM`, 15 hàng trong CSV rộng, đủ 120 giá trị chỉ tiêu trước tiền xử lý.

Mẫu cuối dùng để phân cụm sẽ được quyết định trong notebook 01. Không mặc định rằng mọi quốc gia, mọi năm hay mọi chỉ tiêu đều đủ dữ liệu sau khi lọc mẫu.

## Schema CSV chính

| Cột | Kiểu dự kiến khi đọc | Ý nghĩa |
| --- | --- | --- |
| `country` | Chuỗi | Mã ba ký tự World Bank từ metadata, thường tương ứng ISO3; có thể có mã đặc biệt |
| `country_name` | Chuỗi | Tên hiển thị từ phản hồi WDI, không dùng làm khóa |
| `year` | Số nguyên | Năm quan sát, từ 2010 đến 2024 |
| `is_aggregate` | Số nguyên `0` hoặc `1` | `1` khi metadata quốc gia có `region.id = NA` |
| 8 cột có tên là mã WDI | Số thực, có thể thiếu | Giá trị gốc theo đơn vị từng chỉ tiêu |

Khóa duy nhất của CSV rộng là **(`country`, `year`)**. Trong CSV dài, khóa là **(`country`, `year`, `indicator`)**; các cột còn lại là `country_name`, `is_aggregate`, `indicator_name`, `value`. CSV được ghi bằng UTF-8, dấu phẩy phân cách và dấu chấm thập phân. Ô trống biểu thị giá trị thiếu, **không phải số 0**.

Chỉ 8 cột chỉ tiêu mới là ứng viên đặc trưng. Không đưa `country`, `country_name`, `year` hoặc `is_aggregate` vào phép chuẩn hóa/khoảng cách mặc định. Mọi thay đổi danh sách biến phải được ghi rõ trong metadata tiền xử lý.

## Từ điển chỉ tiêu

| Mã | Chỉ tiêu | Đơn vị | Trang nguồn |
| --- | --- | --- | --- |
| `NY.GDP.PCAP.KD` | GDP bình quân đầu người | USD cố định 2015 | [World Bank](https://data.worldbank.org/indicator/NY.GDP.PCAP.KD) |
| `NY.GDP.MKTP.KD.ZG` | Tăng trưởng GDP | %/năm | [World Bank](https://data.worldbank.org/indicator/NY.GDP.MKTP.KD.ZG) |
| `FP.CPI.TOTL.ZG` | Lạm phát giá tiêu dùng | %/năm | [World Bank](https://data.worldbank.org/indicator/FP.CPI.TOTL.ZG) |
| `SL.UEM.TOTL.ZS` | Thất nghiệp, mô hình ILO | % lực lượng lao động | [World Bank](https://data.worldbank.org/indicator/SL.UEM.TOTL.ZS) |
| `NE.TRD.GNFS.ZS` | Thương mại | % GDP | [World Bank](https://data.worldbank.org/indicator/NE.TRD.GNFS.ZS) |
| `NE.GDI.TOTL.ZS` | Tổng tích lũy vốn | % GDP | [World Bank](https://data.worldbank.org/indicator/NE.GDI.TOTL.ZS) |
| `SP.URB.TOTL.IN.ZS` | Dân số đô thị | % dân số | [World Bank](https://data.worldbank.org/indicator/SP.URB.TOTL.IN.ZS) |
| `NE.CON.GOVT.ZS` | Chi tiêu tiêu dùng cuối cùng của chính phủ | % GDP | [World Bank](https://data.worldbank.org/indicator/NE.CON.GOVT.ZS) |

Tên tiếng Anh, mô tả phương pháp và tổ chức nguồn được lưu trong `du_lieu_tho/nguon_api/metadata/<mã_chỉ_tiêu>.json`. Chỉ tiêu thương mại là tổng xuất và nhập khẩu; tổng tích lũy vốn khác với riêng đầu tư trực tiếp nước ngoài. Thất nghiệp ở đây là ước tính mô hình ILO, không đồng nhất với mọi số liệu thống kê quốc gia.

## CSV được tạo từ JSON như thế nào?

World Bank API trả về một mảng gồm **metadata phân trang** và **danh sách quan sát**. Mỗi chỉ tiêu được tải riêng, một trang đủ 3.990 bản ghi; kết quả kiểm tra `pages = 1` và `total = 3990` được lưu trong manifest.

Việc xuất CSV chỉ gồm đổi định dạng: đưa `date` thành `year`, lấy mã/tên chỉ tiêu và giá trị, gắn metadata thực thể, rồi sắp xếp/pivot thành bảng rộng. **Không loại hàng, không thay thế giá trị thiếu, không làm trơn ngoại lệ, không chuẩn hóa và không chạy mô hình.** Sai khác về cách in chữ số số thực giữa JSON và CSV được kiểm tra bằng đối chiếu giá trị số sau khi đọc lại.

Có 5 nhóm tổng hợp (`XD`, `XM`, `XN`, `XT`, `XY`) có `countryiso3code` trống trong JSON. Vì vậy mã `country` của CSV được xác định bằng cách nối `observation.country.id` với `countries.json → iso2Code`, rồi lấy `metadata.id`. Cách này giữ đúng cả 266 thực thể và tránh gộp nhầm 5 nhóm có mã ISO3 rỗng. Mỗi nền kinh tế không phải nhóm tổng hợp đều được kiểm tra có trường `countryiso3code` khớp metadata; điều này không đồng nghĩa mọi mã World Bank đều là mã ISO chính thức.

Nhóm tổng hợp có `is_aggregate = 1` phải được loại trong bước tiền xử lý. Không chỉ lọc theo độ dài mã, vì mã nhóm tổng hợp cũng có thể dài ba ký tự.

## Tải lại và xác minh

Các URL đầy đủ nằm trong [manifest.json](du_lieu_tho/manifest.json). Chúng dùng API v2 qua HTTPS, `source=2`, `date=2010:2024`, `format=json`, kèm `per_page` và `page`. Metadata quốc gia/metadata chỉ tiêu có URL riêng.

Khi cần cập nhật, Đức triển khai phần thu thập trong notebook 01 và ghi snapshot mới. Dữ liệu WDI có thể được hiệu chỉnh, nên một lần tải lại không được coi là cùng phiên bản chỉ vì cùng khoảng năm. Bảo toàn bản gốc, ghi thời điểm truy cập, kiểm tra đủ trang và tạo lại manifest/checksum nếu thay snapshot.

Kiểm tra checksum từ gốc repo trên macOS/Linux:

```bash
cd du_lieu/du_lieu_tho
shasum -a 256 -c SHA256SUMS
```

## Hợp đồng bàn giao của Đức

| Sản phẩm dự kiến | Quy định |
| --- | --- |
| `du_lieu_sach/wdi_clean.csv` | Một hàng mỗi country–year, không còn nhóm tổng hợp; giữ đơn vị gốc để diễn giải |
| `du_lieu_chuan_hoa/wdi_scaled.csv` | Cùng khóa/cùng mẫu với bảng sạch; chỉ các đặc trưng đã chọn được biến đổi và chuẩn hóa |
| `du_lieu_chuan_hoa/preprocessing_metadata.json` | Nguồn và checksum snapshot, năm/mẫu giữ lại, biến bị loại, `feature_columns` theo thứ tự, xử lý thiếu, biến đổi, tham số chuẩn hóa và phạm vi fit |

Trước bàn giao, kiểm tra khóa không thiếu/trùng, tập khóa giữa hai bảng bằng nhau, toàn bộ đặc trưng mô hình hữu hạn và danh sách cột khớp metadata. Các file này chưa được tạo ở bước khởi tạo.

## Ghi nguồn và quyền sử dụng

Nguồn dữ liệu: **World Bank, World Development Indicators**, [catalog WDI](https://datacatalog.worldbank.org/search/dataset/0037712/world-development-indicators), truy cập ngày 07/11/2026. WDI được catalog công bố theo [CC BY 4.0 và điều khoản bổ sung của World Bank](https://datacatalog.worldbank.org/public-licenses#cc-by); giữ nguyên thông tin tổ chức nguồn trong metadata khi trích dẫn. Việc xuất CSV là thay đổi định dạng và bổ sung khóa từ metadata, chưa làm sạch nội dung dữ liệu.
