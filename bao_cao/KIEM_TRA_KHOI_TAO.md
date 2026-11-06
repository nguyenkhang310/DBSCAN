# Biên bản kiểm tra khởi tạo repository

**Ngày kiểm tra:** 07/11/2026, múi giờ Việt Nam.

**Phạm vi:** bộ khung đồ án và snapshot dữ liệu World Bank WDI; chưa triển khai thuật toán hoặc tiền xử lý dữ liệu.

## 1. Đối chiếu yêu cầu

| Yêu cầu | Kết quả kiểm tra |
| --- | --- |
| Ba thư mục `Duc`, `Khang`, `Khoa` | Có đủ README, notebook và thư mục biểu đồ |
| 4 notebook đúng phân công | Có đủ 01, 02, 03, 04; Đức phụ trách 01 và 04 |
| Notebook chỉ có Markdown | **51 Markdown cell, 0 code cell**, không có cell rỗng |
| Đủ đề mục bắt buộc | 10 mục tiền xử lý, 14 mục DBSCAN, 13 mục đánh giá, 6 mục Việt Nam |
| Có mục tiêu, mục nhỏ, mô tả và kết luận | Có trong từng notebook; kết luận là chỗ dành cho công việc tương lai |
| Notebook hợp lệ | Cả 4 qua `nbformat.validate`, định dạng 4.5, cell ID duy nhất |
| Không có output thực thi | Không có `outputs` hoặc `execution_count` trong các cell |
| Không viết mã Python/mã giả trong notebook | Không có code cell hoặc code block |
| Không tạo `.py` trong nguồn đưa lên Git | 0 file `.py`; `.venv/` và các cache được Git bỏ qua |
| Dữ liệu sạch/chuẩn hóa/kết quả chưa triển khai | Thư mục tương ứng chỉ có `.gitkeep` |
| Nhánh làm việc | `main`, không tạo nhánh riêng theo thành viên |
| README và quy tắc bàn giao | Có tài liệu gốc, dữ liệu, ba thành viên và kết quả chung |
| Cấu trúc thư mục | Cây đầy đủ được ghi trong [README](../README.md#cấu-trúc-repository) |

## 2. Kiểm tra notebook

| Notebook | Markdown cell | Mục nhiệm vụ | Code cell | Xuất HTML |
| --- | ---: | ---: | ---: | --- |
| [01 · Tiền xử lý](../Duc/notebook/01_tien_xu_ly_du_lieu.ipynb) | 12 | 10 | 0 | Thành công |
| [02 · DBSCAN](../Khang/notebook/02_dbscan.ipynb) | 16 | 14 | 0 | Thành công |
| [03 · Đánh giá và so sánh](../Khoa/notebook/03_danh_gia_va_so_sanh.ipynb) | 15 | 13 | 0 | Thành công |
| [04 · Phân tích Việt Nam](../Duc/notebook/04_phan_tich_viet_nam.ipynb) | 8 | 6 | 0 | Thành công |

Mỗi notebook có thêm cell giới thiệu và mục lục ngoài các mục nhiệm vụ. Kernel metadata dùng `Python 3 (ipykernel)`. `nbconvert` xuất đủ 4 bản HTML, có các tiêu đề và mô tả được render; các bản xuất chỉ dùng để kiểm tra, không được đưa vào repo.

## 3. Nguồn dữ liệu và kiểm tra đủ trang

Đã tải **17 phản hồi API gốc**: 8 file giá trị chỉ tiêu, 1 file metadata quốc gia và 8 file metadata chỉ tiêu. Các phản hồi được giữ nguyên byte, có URL và thời điểm tải trong [manifest](../du_lieu/du_lieu_tho/manifest.json).

- 8 file chỉ tiêu đều thuộc API source `2`, mỗi file **3.990 bản ghi**.
- Metadata phân trang của mỗi phản hồi đều có `page = 1`, `pages = 1`; `total` khớp số bản ghi đọc được.
- Tất cả file dữ liệu chỉ tiêu có `lastupdated = 2026-10-08`.
- Phạm vi năm đủ 2010–2024; mỗi thực thể có 15 quan sát cho mỗi chỉ tiêu, kể cả giá trị thiếu.
- Metadata quốc gia có 296 thực thể; dữ liệu chỉ tiêu của snapshot sử dụng 266 thực thể trong số đó.
- Mã/tên chỉ tiêu được đối chiếu với metadata và từ điển chỉ tiêu.

Không phát hiện bản ghi trùng khóa thực thể–năm–chỉ tiêu, mã không ghép được với metadata, giá trị số vô hạn hoặc thiếu trang API.

## 4. Đối chiếu CSV với API

| Hạng mục | Kết quả |
| --- | --- |
| CSV rộng | 3.990 hàng, 12 cột, khóa `country` + `year` duy nhất |
| CSV dài | 31.920 hàng, 7 cột, khóa `country` + `year` + `indicator` duy nhất |
| Giá trị CSV rộng đối chiếu API | **31.920/31.920 khớp** sau khi đọc lại thành số |
| Giá trị CSV dài đối chiếu API | **31.920/31.920 khớp**, cùng tên chỉ tiêu, tên thực thể và cờ nhóm tổng hợp |
| Giá trị thiếu | **3.354** giá trị `null` giữ nguyên thành ô CSV trống |
| Phạm vi thực thể | **217** quốc gia/vùng lãnh thổ và **49** nhóm tổng hợp, không loại mẫu ở bước xuất CSV |
| Trường ISO3 trống | Bảo toàn đúng 5 nhóm `XD`, `XM`, `XN`, `XT`, `XY` nhờ đối chiếu metadata |
| Việt Nam | **15 hàng, 120/120 giá trị**, không thiếu trong snapshot gốc |
| Mã nguồn | Trường `countryiso3code` của mọi nền kinh tế không tổng hợp khớp mã metadata |
| Checksum | **19/19 file khớp SHA-256**, gồm 2 CSV và 17 JSON gốc |

Việc xuất CSV chỉ thay đổi định dạng, sắp xếp/pivot và gắn metadata định danh. Không thay thế số thiếu, xóa thực thể, làm sạch ngoại lệ, chuẩn hóa hoặc chạy phân cụm.

### Thống kê ô thiếu để kiểm chứng snapshot

Các số dưới đây tính trên **toàn bộ dữ liệu gốc, bao gồm nhóm tổng hợp**, dùng để kiểm kê file đã tải, chưa phải báo cáo EDA hoặc quyết định loại biến.

| Chỉ tiêu | Bản ghi | Giá trị thiếu |
| --- | ---: | ---: |
| `NY.GDP.PCAP.KD` | 3.990 | 148 |
| `NY.GDP.MKTP.KD.ZG` | 3.990 | 137 |
| `FP.CPI.TOTL.ZG` | 3.990 | 498 |
| `SL.UEM.TOTL.ZS` | 3.990 | 474 |
| `NE.TRD.GNFS.ZS` | 3.990 | 632 |
| `NE.GDI.TOTL.ZS` | 3.990 | 732 |
| `SP.URB.TOTL.IN.ZS` | 3.990 | 15 |
| `NE.CON.GOVT.ZS` | 3.990 | 718 |
| **Tổng** | **31.920** | **3.354** |

## 5. Môi trường và khả năng mở notebook

Đã tạo môi trường ảo riêng bằng **Python 3.12.9 trên macOS arm64**, cài toàn bộ [requirements.txt](../requirements.txt), kiểm tra phiên bản và import đủ 12 dependency trực tiếp. `python -m pip check` trả về **No broken requirements found**. Các dependency trực tiếp được pin; đây chưa phải lockfile cho toàn bộ dependency gián tiếp.

Jupyter Notebook được khởi động cục bộ để kiểm tra. Với cả 4 notebook:

- Contents API trả đúng loại `notebook`, nội dung JSON và toàn bộ cell Markdown.
- Trang `/notebooks/<đường_dẫn>` trả **HTTP 200**.
- Xuất HTML bằng `nbconvert` thành công, giữ đủ đề mục và tiếng Việt.

**Giới hạn xác minh giao diện:** kết nối Browser của phiên làm việc không khởi tạo được, nên chưa kiểm tra trực quan thao tác bấm/chỉnh sửa trên giao diện Jupyter hoặc mở trực tiếp trong VS Code. Định dạng notebook, metadata, khả năng render HTML và khả năng phục vụ bằng Jupyter đã được kiểm tra. Hướng dẫn VS Code trong README dựa trên việc mở notebook chuẩn và chọn kernel `.venv`.

## 6. Tài liệu và vệ sinh Git

Đã kiểm tra **66 liên kết nội bộ** trong Markdown và notebook, gồm cả liên kết tới mục trong README; đối chiếu số lượng mẫu, tên file và đường dẫn bàn giao giữa các tài liệu. Những sản phẩm chưa tạo được ghi rõ là **dự kiến**, không có nhãn, biểu đồ hay điểm số giả.

Kiểm tra nguồn dự kiến đưa lên Git không chứa đường dẫn cá nhân của máy, file môi trường ảo, checkpoint, conflict marker hoặc mẫu khóa truy cập phổ biến. `.gitignore` bao gồm Python/Jupyter, môi trường, file cấu hình nhạy cảm, VS Code và macOS. Kiểm tra whitespace của Git được thực hiện trước commit.

## 7. Phạm vi nghiệm thu

Bộ khung đủ để clone, cài môi trường và bắt đầu triển khai trong notebook. Dữ liệu CSV/JSON gốc có nguồn và đối chiếu đầy đủ. Hiệu quả DBSCAN, tham số tối ưu, độ ổn định, điểm số so sánh và kết luận kinh tế **chưa được kiểm chứng**, vì thuộc giai đoạn thực hiện đồ án sau khởi tạo.
