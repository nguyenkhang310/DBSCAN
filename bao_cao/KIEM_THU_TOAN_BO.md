# Kiểm chứng luồng dữ liệu và mô hình

## Phạm vi và môi trường

Bốn notebook được thực thi theo thứ tự 01 → 02 → 03 → 04, mỗi notebook dùng kernel mới. Môi trường Python 3.12.9, NumPy 2.5.4, pandas 3.1.1, scikit-learn 1.9.1; các dependency trực tiếp được cố định trong requirements.txt. pip check không phát hiện dependency hỏng.

| Notebook | Code cell | Dòng code | Một lượt thực thi |
| --- | ---: | ---: | ---: |
| 01_tien_xu_ly_du_lieu | 13 | 190 | 5.21 s |
| 02_dbscan | 23 | 443 | 11.34 s |
| 03_danh_gia_va_so_sanh | 12 | 189 | 9.04 s |
| 04_phan_tich_viet_nam | 7 | 101 | 2.73 s |

Mỗi code cell tối đa 40 dòng. Không có comment thừa, import chưa dùng hoặc hàm chưa được gọi. Phần huấn luyện ngoài mẫu làm tăng số dòng ở notebook 02 vì bổ sung phép chia, chuẩn hóa train, chọn validation và đánh giá test; các bước này được giữ riêng để kiểm tra rò rỉ dữ liệu.

## Kiểm tra dữ liệu

- Checksum 19 file nguồn; CSV rộng/dài khớp giá trị và khóa, metadata xác nhận loại nhóm tổng hợp.
- Nội suy có tám ca kiểm thử: khoảng ngắn/dài, biên, toàn thiếu và chuỗi một điểm. Mọi giá trị gốc không thiếu được bảo toàn; 32 ô nội suy có nhật ký, 10 ô thuộc mẫu cuối.
- Mẫu sạch có 2.315 hàng, 162 nền kinh tế, khóa country–year duy nhất; mọi đặc trưng hữu hạn. Chuẩn hóa được tái tạo từ log/signed-log và tham số metadata.
- Checksum đầu vào được kiểm tra trước phân cụm; đọc UTF-8 và xuất CSV LF để nhất quán giữa các hệ điều hành.

## Kiểm tra thuật toán và chỉ số

- DBSCAN: tám ca biết trước, 11 đầu vào sai, 36 cấu hình giả lập, trường hợp border nằm giữa hai cụm.
- Bản tự viết được đối chiếu độc lập với scikit-learn trên WDI toàn panel và train: ARI = 1, cùng core và noise.
- Kiểm tra mật độ core, border có core cùng cụm và noise không nằm trong eps của core.
- Mọi Silhouette, DBI và CH trong bảng đối chứng được tính lại trên đúng tập mẫu và nhãn xuất; không dùng điểm số của hai mẫu khác nhau như cùng phạm vi.
- Ba ca mẫu rỗng, một cụm và mỗi điểm một nhãn kiểm tra xử lý chỉ số không hợp lệ. Test ngoài mẫu có một nhãn nên ba chỉ số đều N/A, không được điền 0.

## Kiểm tra huấn luyện ngoài mẫu

- Phép chia seed 42 tạo đúng 97/32/33 quốc gia, tương ứng 1.397/464/454 điểm; không trùng quốc gia giữa ba tập.
- Trung vị/IQR của scaler được fit lại từ riêng 1.397 điểm train và so với cấu hình đã xuất. Không dùng scaler toàn panel cho thí nghiệm này.
- 90 cấu hình train/validation được lưu; bảng tìm kiếm không có cột test. Cấu hình chọn được tái tính từ validation bằng đúng quy tắc đã khai báo.
- Nhãn validation/test được tái tạo độc lập bằng core train gần nhất trong eps; điểm ngoài bán kính bị từ chối. Không fit hay tạo cụm từ test.
- Kiểm tra hai ca gán điểm: điểm đúng biên eps và mô hình không có core. Khóa các file nhãn ngoài mẫu khớp phép chia và dữ liệu sạch.

## Tái lập và tài liệu

Chuỗi được chạy từ cả gốc repo lẫn thư mục notebook với kernel mới. **51 file CSV/JSON/PNG** được đối chiếu SHA-256 qua hai lượt; không có thay đổi đầu ra. Mọi code cell có execution count liên tục, không có output lỗi hoặc cảnh báo. Xuất HTML được dùng để kiểm tra nội dung và công thức; biểu đồ được kiểm tra trục/chú giải/bố cục.

Các file hình sao chép trùng, bảng hồ sơ dạng rộng trùng thông tin dạng dài và thư viện plotly/wbgapi không được sử dụng đã được bỏ. Báo cáo liên kết trực tiếp tới hình gốc. Dữ liệu/API gốc, metadata, checksum và bảng kiểm chứng được giữ làm bằng chứng nguồn và kết quả.

## Kết luận kiểm chứng

Luồng tính toán, tham số, phép chia và chỉ số được tái lập. **Chất lượng mô hình chưa đạt yêu cầu tổng quát hóa tốt**: toàn panel phủ 32,79%, test phủ 19,82% với một nhãn cụm; không có accuracy % vì thiếu nhãn chuẩn. Kết luận kỹ thuật và kết luận nghiên cứu được phân biệt trong [báo cáo kết quả](BAO_CAO_KET_QUA.md).
