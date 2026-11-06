# Quy ước kết quả chung

Các thư mục con hiện chỉ có `.gitkeep`. Tài liệu này quy định sản phẩm sẽ được tạo khi nhóm bắt đầu triển khai, **chưa xác nhận có nhãn hoặc điểm số**.

## Đường đi của kết quả

| Thư mục | Người phụ trách | Nội dung dự kiến |
| --- | --- | --- |
| [dbscan/](dbscan/) | Khang | Nhãn cuối, tham số, các lần thử và độ nhạy |
| [danh_gia/](danh_gia/) | Khoa | So sánh DBSCAN, K-Means, Agglomerative và GMM |
| [ho_so_cum/](ho_so_cum/) | Khoa | Mô tả các cụm theo chỉ tiêu kinh tế ở đơn vị gốc |
| [phan_tich_nhieu/](phan_tich_nhieu/) | Khoa | Danh sách và diễn giải các quan sát noise |
| [bieu_do_bao_cao/](bieu_do_bao_cao/) | Cả nhóm | Biểu đồ hoàn thiện có tên, đơn vị, chú giải và nguồn |

## Nhãn DBSCAN cuối

File dự kiến: `dbscan/dbscan_labels.csv`.

| Cột | Quy định |
| --- | --- |
| `country` | Mã ba ký tự World Bank của nền kinh tế, khớp dữ liệu sạch |
| `year` | Số nguyên, khớp mẫu đầu vào |
| `cluster` | Số nguyên; `-1` là noise, nhãn không âm là các cụm |
| `point_type` | Một trong `core`, `border`, `noise` |

Khóa (`country`, `year`) phải duy nhất, không thiếu, không còn nhóm tổng hợp và khớp đúng tập khóa của dữ liệu chuẩn hóa đã dùng. `cluster = -1` phải tương ứng `point_type = noise`. Nhãn cuối chỉ chứa cấu hình đã chọn, không trộn nhiều run vào cùng khóa.

`tham_so_da_chon.json` cần ghi phạm vi năm, cách fit từng năm hay gộp panel, metric, `eps`, `min_samples`, nguồn/checksum dữ liệu tiền xử lý, thứ tự đặc trưng, phiên bản thư viện, quy ước tính lân cận và lý do chọn cấu hình. Nếu fit riêng từng năm, lưu cấu hình theo năm và mô tả cách diễn giải nhãn giữa các năm.

`grid_search.csv` cần có `run_id`, phạm vi năm, tham số, số mẫu, số cụm không kể noise, số/tỷ lệ noise, chỉ số hợp lệ và ghi chú trường hợp không tính được. `run_id` phân biệt thử nghiệm; không thay thế khóa bàn giao country–year.

## Bảng đánh giá

File dự kiến: `danh_gia/so_sanh_thuat_toan.csv`. Mỗi dòng cần xác định thuật toán, cấu hình/run, phạm vi năm, tập mẫu đánh giá, số mẫu đầu vào, số mẫu được đánh giá, `coverage`, số cụm, tỷ lệ nhiễu, Silhouette, Davies-Bouldin, Calinski-Harabasz và ghi chú.

- **Silhouette:** cao hơn thường tốt hơn; **Davies-Bouldin:** thấp hơn thường tốt hơn; **Calinski-Harabasz:** cao hơn thường tốt hơn trong cùng phạm vi so sánh.
- Chỉ tính các chỉ số trên tập đánh giá có `2 ≤ số nhãn < số mẫu`. Trường hợp không hợp lệ ghi `N/A` kèm lý do, không điền 0 để giả lập điểm số.
- Phép đánh giá chính của DBSCAN loại noise khỏi các chỉ số nội bộ và luôn báo số mẫu/độ phủ. Không coi noise là một cụm có ý nghĩa kinh tế.
- Thêm phép so sánh của mọi thuật toán trên **cùng tập con non-noise của DBSCAN**; giữ nhãn đã fit trên toàn mẫu, rồi kiểm tra lại điều kiện số nhãn trên tập con. Ghi rõ đây là đánh giá có điều kiện trên tập con đó.
- Báo riêng cấu hình và tỷ lệ nhiễu. Một điểm số cao trên rất ít mẫu không đủ chứng minh thuật toán tốt hơn.

## Hồ sơ cụm và noise

Ghép nhãn về dữ liệu sạch theo country–year để phân tích ở đơn vị gốc. Báo quy mô cụm, mức điển hình, độ phân tán, quốc gia/năm đại diện và phạm vi dữ liệu. Nhãn số của các mô hình khác nhau không nhất thiết tương ứng, kể cả khi cùng là `0` hoặc `1`.

Danh sách noise phải giữ mã quốc gia, năm và các đặc trưng liên quan; mô tả khả năng do chất lượng dữ liệu, thang đo, tham số hoặc khác biệt kinh tế. Mọi diễn giải về Việt Nam hoặc sự kiện kinh tế cần có dữ liệu/bối cảnh hỗ trợ, không chỉ dựa vào nhãn `-1`.

## Trước khi đưa kết quả vào báo cáo

Kiểm tra nguồn dữ liệu và cấu hình truy vết được, các bảng dùng đúng tập khóa, biểu đồ có đơn vị/chú giải và nhận xét phù hợp phạm vi mẫu. Lưu biểu đồ cá nhân ở thư mục từng thành viên, rồi đưa phiên bản được chọn vào `bieu_do_bao_cao/`.
