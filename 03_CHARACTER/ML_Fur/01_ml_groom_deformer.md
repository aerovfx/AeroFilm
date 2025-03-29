# Dự Đoán Biến Dạng Lông Thú Bằng Machine Learning

## Tổng Quan
Mục tiêu là dự đoán cách lông biến dạng trên nhân vật hoặc sinh vật bằng mô hình machine learning thay vì sử dụng mô phỏng đắt đỏ và thiết lập thủ công.

## Vấn Đề
Việc biến dạng lông một cách đơn giản có thể gây ra lỗi giao cắt giữa các lớp lông, đặc biệt ở khu vực khớp. Điều này khiến lông phía trên xuyên qua lớp lông bên dưới, làm mất đi độ tự nhiên. Để giải quyết vấn đề này thông thường cần mô phỏng phức tạp và nhiều bước xử lý hậu kỳ.

## Giải Pháp
Sử dụng mô hình machine learning để dự đoán cách các đường dẫn (guides) của lông biến dạng dựa trên vị trí khung xương (rig). Mô hình học cách liên kết dữ liệu xoay của từng khớp với sự dịch chuyển của các đường dẫn trong mỗi tư thế.

### Quy trình:
1. Xác định giới hạn của các khớp trên rig.
2. Tạo nhiều tư thế ngẫu nhiên (khoảng 3000 hoặc hơn) dựa trên giới hạn này.
3. Mô phỏng sự biến dạng của lông cho mỗi tư thế.
4. Nén dữ liệu bằng PCA để giảm số lượng biến dạng cần lưu trữ.
5. Lưu bộ dữ liệu tiền xử lý vào ổ đĩa.
6. Huấn luyện mô hình ML trong Houdini bằng TOPs.

## Quá Trình Tạo Dữ Liệu

### Giới Hạn Khớp
Giới hạn này có thể cố định (ví dụ: 30 độ) hoặc được tự động thiết lập dựa trên các đoạn chuyển động có sẵn.

### Ngẫu Nhiên Hóa Tư Thế
Houdini 20.5 giới thiệu node `ml pose generate SOP` để tạo các tư thế ngẫu nhiên theo phân phối Gaussian.

### Vòng Lặp Mô Phỏng
Chạy qua tất cả các tư thế để mô phỏng sự biến dạng hợp lý cho các đường dẫn lông. Điều kiện quan trọng:
- Kết quả phải có tính quyết định, không phụ thuộc vào động lực học như rung lắc hay dao động.
- Mối quan hệ giữa đầu vào và đầu ra phải mượt mà.

Sử dụng mô phỏng quasi-static với Vellum và thuật toán tránh giao cắt bằng trường vận tốc.

### Tính Toán Dịch Chuyển Ở Trạng Thái Nghỉ
Sau khi mô phỏng xong, đưa các tư thế về trạng thái nghỉ và tính toán sự khác biệt giữa đường dẫn biến dạng với trạng thái ban đầu.

### Lưu Trữ Dữ Liệu
Mỗi tư thế sẽ được lưu lại thành một cặp dữ liệu huấn luyện, bao gồm vị trí khung xương và dịch chuyển của các điểm trên đường dẫn.

## Nén Dữ Liệu Bằng PCA
Dữ liệu biến dạng được nén bằng PCA để giảm số lượng thông tin cần lưu trữ. Thay vì lưu 100.000 vị trí điểm, mô hình chỉ cần dự đoán một tập hợp nhỏ các trọng số cần thiết để tái tạo lại biến dạng ban đầu.

## Huấn Luyện Mô Hình
Huấn luyện được thực hiện trong TOPs, sử dụng node `ml regression train TOP`, một wrapper của PyTorch. Các tham số quan trọng:
- **Số lớp ẩn**: Kích thước của mạng.
- **Chiều rộng lớp ẩn**: Số lượng neuron trong mỗi lớp.
- **Batch size**: Số lượng mẫu xử lý trước khi điều chỉnh trọng số.
- **Learning rate**: Kích thước bước điều chỉnh mô hình.

Có thể thực hiện "wedging" (tối ưu tham số) để tìm ra cấu hình tốt nhất.

## Dự Đoán (Inference)
Dữ liệu đầu vào cần được xử lý giống như trong giai đoạn huấn luyện:
1. Chuyển đổi tư thế mới của rig thành đầu vào phù hợp.
2. Áp dụng mô hình để dự đoán trọng số cần thiết.
3. Dùng PCA để tái tạo lại dịch chuyển của lông.
4. Áp dụng dịch chuyển lên đường dẫn lông.

## Kết Quả
Mô hình có thể dự đoán sự biến dạng của lông với độ chính xác cao, giúp tiết kiệm thời gian và tài nguyên so với mô phỏng truyền thống. 
