**Bài Giảng: Procedural Thành Phố Trong Houdini - Tuần 1**

### 1. Giới Thiệu Về Procedural Modeling Trong Houdini

Chào mừng các bạn đến với khóa học tạo thành phố theo phương pháp procedural trong Houdini. Trong bài giảng đầu tiên, chúng ta sẽ khám phá các nguyên tắc cơ bản của modeling thủ tục, những công cụ quan trọng trong Houdini và cách áp dụng chúng để tạo ra một thành phố động và linh hoạt.

### 2. Procedural Modeling Trong Houdini

Houdini cho phép chúng ta xây dựng các mô hình 3D bằng cách sử dụng các node và biến số, thay vì phải thao tác bằng tay trực tiếp như các phần mềm khác. Điều này giúp tạo ra các mô hình linh hoạt, dễ chỉnh sửa và tái sử dụng. Trong bài giảng này, chúng ta sẽ tìm hiểu:
- **Network Editor**: Cách sửa đổi và lắp ghép các node.
- **SOPs (Surface Operators)**: Xử lý hình dạng bề mặt.
- **Channel Referencing**: Kết nối các thông số giữa các node.

### 3. Tạo Cơ Sở Thành Phố

Bước đầu tiên trong việc xây dựng thành phố là tạo cấu trúc cơ bản của các con đường và khối nhà. Chúng ta sẽ:
- Dùng **Curve SOP** để tạo các tuyến đường.
- Chuyển đổi curve thành mặt phẳng bằng **PolyExtrude SOP**.
- Dùng **Copy to Points SOP** để tạo các tòa nhà dọc theo tuyến đường.

### 4. Dùng VEX Để Tối Ưu Quy Trình

Houdini cung cấp VEX, một ngôn ngữ lập trình giúp xử lý các biến hình một cách linh hoạt. Các bạn có thể dùng VEX để:
- Tạo các thành phần ngẫu nhiên như chiều cao tòa nhà.
- Xử lý vị trí của tòa nhà sao cho phù hợp với cấu trúc đường.

### 5. Bài Tập Và Đề Xuất

Bài tập dành cho tuần này:
1. Tạo một layout cơ bản với các con đường và tòa nhà sử dụng SOPs.
2. Thêm sự ngẫu nhiên và tùy chỉnh cho chiều cao tòa nhà bằng VEX.
3. Xuất file thành phố để dùng trong Unreal Engine hoặc Unity.

Trong tuần tới, chúng ta sẽ tìm hiểu về việc thêm chi tiết và texture cho các tòa nhà.

