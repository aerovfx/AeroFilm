ML Groom Deformer là một hướng dẫn về cách sử dụng các nút máy học (ML) dựa trên ví dụ, được phát hành cùng Houdini 20.5, để xây dựng một công cụ biến dạng lông. Hệ thống này dựa trên ML Deformer H20.5 và mở rộng chức năng để làm việc với lông.  ￼
https://media.sidefx.com/uploads/tutorial/h20_5/jakobr/ML_Groom_Deformer/previewimage.jpg
Ý tưởng chung

Mục tiêu là dự đoán cách lông biến dạng trên một nhân vật hoặc sinh vật bằng cách sử dụng mô hình máy học, thay vì dựa vào các mô phỏng tốn kém và các thiết lập thủ tục.

Vấn đề

Khi biến dạng tóc một cách đơn giản hoặc tuyến tính, đặc biệt xung quanh các khu vực khớp, thường xảy ra nhiều vấn đề giao nhau, nơi tóc phía trên khớp xuyên qua lớp lông phía dưới. Để đạt được sự xếp lớp hướng dẫn tốt và duy trì thể tích, thường cần đến mô phỏng tốn kém và các bước xử lý hậu kỳ.
https://media.sidefx.com/uploads/tutorial/h20_5/jakobr/ML_Groom_Deformer/01.gif
Giải pháp
https://media.sidefx.com/uploads/tutorial/h20_5/jakobr/ML_Groom_Deformer/02.png
Mục tiêu là dự đoán sự biến dạng cần áp dụng cho các hướng dẫn dựa trên vị trí rig bằng mô hình ML. Mô hình học cách ánh xạ từ dữ liệu xoay của mỗi khớp rig đến sự dịch chuyển xấp xỉ của các hướng dẫn cho mỗi tư thế.

Quy trình chung
	1.	Định nghĩa giới hạn khớp trên rig (giá trị cố định hoặc tự động theo cách thủ tục)
	2.	Tạo một loạt các tư thế ngẫu nhiên dựa trên các giới hạn khớp này (khoảng 3000 hoặc hơn để có độ phủ tốt)
	3.	Mô phỏng một biến dạng hướng dẫn chuẩn cho mỗi tư thế
	4.	Thu thập tất cả các biến dạng và nén dữ liệu vào không gian con PCA
	5.	Lưu toàn bộ tập dữ liệu đã tiền xử lý vào đĩa
	6.	Huấn luyện mô hình ML trong TOPs
https://media.sidefx.com/uploads/tutorial/h20_5/jakobr/ML_Groom_Deformer/03.gif
Tạo dữ liệu

Để tạo tất cả dữ liệu huấn luyện, cần hai yếu tố:
	1.	Tư thế rig ngẫu nhiên: Sử dụng nút ML Pose Generate để tạo các tư thế ngẫu nhiên dựa trên giới hạn khớp.  ￼
	2.	Biến dạng hướng dẫn chuẩn: Mô phỏng biến dạng hướng dẫn cho mỗi tư thế để tạo dữ liệu đầu ra mục tiêu.

Nén PCA

Sau khi thu thập tất cả các biến dạng, sử dụng Phân tích Thành phần Chính (PCA) để nén dữ liệu vào không gian con, giảm số lượng thành phần cần thiết để biểu diễn dữ liệu.

Huấn luyện mô hình

Sử dụng các nút ML trong Houdini để huấn luyện mô hình trên tập dữ liệu đã nén, cho phép dự đoán sự biến dạng của lông dựa trên tư thế rig đầu vào.

Kết luận

Bằng cách sử dụng các công cụ ML trong Houdini 20.5, có thể tạo ra một hệ thống biến dạng lông hiệu quả, giảm sự phụ thuộc vào các mô phỏng tốn kém và các thiết lập thủ tục phức tạp.