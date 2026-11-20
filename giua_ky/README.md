# Báo cáo giữa kỳ - DBSCAN

[Notebook giữa kỳ](DBSCAN%20gi%E1%BB%AFa%20k%E1%BB%B3.ipynb) giải thích DBSCAN và minh họa trên 12 nền kinh tế giả lập. Mỗi điểm có hai tọa độ: tăng trưởng GDP và tỷ lệ thất nghiệp. Dữ liệu và biểu đồ được lưu trong notebook.

| Phần | Thành viên | MSSV |
| --- | --- | --- |
| Dữ liệu và vùng lân cận | Huỳnh Cao Trung Đức | 24133012 |
| Định nghĩa và cài đặt DBSCAN | Bùi Nguyễn Nguyên Khang | 24133902 |
| Chạy demo và đối chiếu kết quả | Phạm Đức Khoa | 24149170 |

Thuật toán được cài bằng Python và NumPy. Pandas dùng để trình bày bảng và Matplotlib dùng để vẽ biểu đồ. Cấu hình minh họa là eps = 0,55 và min_samples = 4.

| Nhãn | Điểm lõi | Điểm biên | Điểm nhiễu | Tổng |
| --- | ---: | ---: | ---: | ---: |
| 0 | 2 | 3 | 0 | 5 |
| 1 | 2 | 3 | 0 | 5 |
| -1 | 0 | 0 | 2 | 2 |

Phương pháp tham khảo [bài báo gốc của Ester và cộng sự (1996)](https://cdn.aaai.org/KDD/1996/KDD96-037.pdf).
