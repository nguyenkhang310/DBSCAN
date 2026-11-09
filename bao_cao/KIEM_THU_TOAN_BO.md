# Kiểm thử toàn bộ luồng notebook

Ngày kiểm tra: **09/11/2026**. Python 3.12.9, môi trường theo requirements.txt.

## Thay đổi chính

- Bỏ mô tả lặp, comment thừa, hàm đệ quy suy luận cấu hình và các lớp xử lý tổng quát không cần thiết.
- Nội suy đúng toàn khoảng thiếu: bên trong tối đa 2 năm, ở biên đúng 1 năm. Không lấp một phần khoảng thiếu dài. Mẫu sửa còn **2.315** hàng, thay cho **2.334**; tất cả kết quả phía sau được tạo lại.
- CSV đầu ra dùng LF và checksum mới; `.gitattributes` giữ xuống dòng nhất quán.
- Hoàn thiện Việt Nam/Đông Nam Á và bản đồ ngoại tuyến. Dùng mã ADM0_A3, tránh mã WB cũ ROM/TMP cho Romania/Timor-Leste.

## Chạy và tái lập

| Notebook | Dòng code | Code cell | Lần chạy từ gốc repo |
| --- | ---: | ---: | ---: |
| 01_tien_xu_ly_du_lieu | 185 | 13 | 5.52s |
| 02_dbscan | 365 | 19 | 10.05s |
| 03_danh_gia_va_so_sanh | 198 | 12 | 10.54s |
| 04_phan_tich_viet_nam | 105 | 7 | 3.11s |

Đã chạy cả chuỗi 01 → 02 → 03 → 04 bằng kernel mới, rồi chạy lại từ từng thư mục notebook. So sánh SHA-256 **54 file CSV/JSON/PNG** của hai lượt để xác nhận kết quả tái lập. Không dùng trạng thái còn lại từ phiên trước.

## Kiểm tra

| Phạm vi | Kiểm tra |
| --- | --- |
| Nguồn | Checksum 19 file, bảng rộng/dài khớp, không sửa dữ liệu thô |
| Nội suy | 8 ca: khoảng ngắn/dài, biên, toàn thiếu, chuỗi một điểm; không thay giá trị gốc có sẵn |
| Chuẩn hóa | Khóa khớp; không NaN/inf; trung vị 0, IQR 1; tái tạo đúng từ metadata |
| DBSCAN | 8 ca biết đáp án, 11 ca đầu vào sai, 36 đối chiếu giả lập; khớp scikit-learn trên WDI |
| Nhãn xuất | Core đúng mật độ; border có core cùng cụm; noise không gần core; khóa một-một |
| Đánh giá | Ba chỉ số tính lại trên đúng mẫu; 54 cấu hình đối chứng; GMM chọn trong mô hình hội tụ |
| Việt Nam | 15 năm; láng giềng cùng năm; độ phủ đủ 11 mã Đông Nam Á |
| Bản đồ | Ranh giới đọc từ file; xuất riêng 12 nền kinh tế không có hình học ở tỷ lệ 1:110m |
| Notebook | Đúng 10/14/13/6 đề mục; mọi code cell thực thi, không có output lỗi/cảnh báo |
| Repository | Không có .py/checkpoint/môi trường ảo trong nguồn; kiểm tra liên kết và diff trước commit |

Các hình đã được xuất lại; kiểm tra bố cục tương quan, phân cụm, so sánh và bản đồ. Bản đồ tỷ lệ thấp không thể hiện một số nước nhỏ, không đồng nghĩa thiếu dữ liệu kinh tế.

## Kết quả và giới hạn

DBSCAN có 4 cụm, 759 non-noise và 1556 noise (67.21%); Silhouette non-noise 0.1889. Chưa đạt mục tiêu độ phủ trong lưới đã thử. Kiểm thử đúng thuật toán không đồng nghĩa mô hình có chất lượng cao. Các năm cùng quốc gia không độc lập; kết quả hồi cứu không chứng minh khả năng dự báo hoặc nguyên nhân kinh tế.
