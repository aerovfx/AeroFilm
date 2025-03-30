**Giáo trình tuần 3** về chủ đề **Procedural Modeling trong Houdini**

---

### **Tuần 3: Xây dựng HDA (Houdini Digital Asset) và Tối ưu hóa Workflow**
#### **Mục tiêu**:  
- Hiểu cách tạo và quản lý HDA.  
- Thêm các tham số điều khiển (parameters) và tối ưu giao diện người dùng.  
- Tích hợp caching, materials và các tính năng nâng cao.  

---

### **Phần 1: Tạo HDA (Houdini Digital Asset)**
1. **Giới thiệu về HDA**:  
   - HDA là một "tài sản kỹ thuật số" trong Houdini, có thể tái sử dụng và chia sẻ giữa các artist.  
   - Khi chỉnh sửa HDA, mọi thay đổi sẽ tự động cập nhật cho tất cả người dùng đang sử dụng asset đó.  

2. **Các bước tạo HDA**:  
   - **Bước 1**: Chuột phải vào node cần chuyển đổi → **Create Digital Asset**.  
   - **Bước 2**: Đặt tên (vd: `Building Generator`), chọn thư mục lưu (vd: `OTL`), tắt các flag không cần thiết (Author, Branch).  
   - **Bước 3**: Nhấn **Create** → Asset được lưu dưới dạng file `.otl`.  

3. **Quản lý phiên bản**:  
   - **Lock/Unlock Asset**:  
     - Khi asset bị **khóa** (biểu tượng ổ khóa), nó đọc từ file trên disk.  
     - **Mở khóa** để chỉnh sửa trực tiếp trong scene.  
   - **Lưu ý**: Luôn sao lưu HDA trước khi cập nhật để tránh ảnh hưởng đến người dùng khác.  

---

### **Phần 2: Thêm Parameters và Tối ưu Giao diện**
1. **Thêm Parameters từ Node con**:  
   - **Ví dụ**: Thêm tham số điều khiển kích thước sàn nhà:  
     - Mở **Type Properties** → Kéo thả tham số `grid_size` từ node con vào folder **Controls**.  
   - **Giới hạn giá trị**:  
     - Đặt `Minimum = 2`, `Maximum = 10` để ngăn người dùng nhập giá trị không hợp lệ.  

2. **Tạo Menu lựa chọn**:  
   - **Ví dụ**: Menu chọn loại sàn (Grid/Curve):  
     - Thêm **Ordered Menu** → Đặt tên `Floor_Type`.  
     - Thiết lập giá trị: `0 = Grid`, `1 = Curve`.  
   - **Ẩn/Hiện Parameters**:  
     - Sử dụng điều kiện `hideWhen`/`disableWhen` (vd: ẩn `grid_size` nếu `Floor_Type = 1`).  

3. **Tổ chức Parameters**:  
   - Tạo các folder phân loại: **Ground Floor**, **Second Floor**, **Roof Controls**.  
   - Thêm **Spacer** hoặc **Separator** để tạo khoảng cách giữa các nhóm.  

---

### **Phần 3: Tích hợp Caching và Materials**
1. **Caching với Alembic**:  
   - Thêm node **Alembic Output** → Thiết lập đường dẫn lưu file `.abc`.  
   - Tích hợp nút **Save to Disk** vào giao diện HDA để người dùng dễ dàng lưu cache.  

2. **Gán Materials**:  
   - Tạo **Material Network** (vd: `Plaster_Clean`, `Plaster_Dirty`).  
   - Sử dụng **Attribute Wrangle** để gán material theo nhóm:  
     ```python
     s@mat = "Plaster";  // Gán material "Plaster" cho primitives
     ```  
   - Đưa tham số chọn material lên giao diện HDA.  

---

### **Phần 4: Nâng cao - Thêm Tính năng Procedural**
1. **Tạo Biến thể Ngẫu nhiên**:  
   - Sử dụng **Attribute Randomize** để xáo trộn hướng (`orient`) và kích thước (`pscale`) của các đối tượng.  
   - **Ví dụ**:  
     ```python
     v@orient = rand(@ptnum) * 360;  // Random hướng
     f@pscale = fit01(rand(@ptnum), 0.8, 1.2);  // Random tỷ lệ
     ```  

2. **Thêm Chi tiết Hư hỏng**:  
   - Dùng **Boolean Node** để cắt xén các cạnh.  
   - Sử dụng **VEX Wrangle** để xóa ngẫu nhiên điểm (points) dựa trên threshold:  
     ```python
     if (rand(@ptnum) < chf("threshold")) removepoint(0, @ptnum);
     ```  

3. **Tích hợp Đường cong Tùy chỉnh**:  
   - Tạo **Dive Target** để người dùng chỉnh sửa đường cong mà không cần mở khóa HDA.  
   - Thêm **Object Merge** để kết nối dữ liệu từ input bên ngoài.  

---

### **Bài tập về nhà**:  
1. Hoàn thiện HDA: Đưa tất cả tham số quan trọng lên giao diện người dùng.  
2. Tạo menu điều khiển cho:  
   - Số tầng (`floor_amount`).  
   - Loại mái nhà (`roof_type`).  
   - Toggle hiển thị ống khói (`chimney_toggle`).  
3. Áp dụng caching và materials cho asset.  

---

### **Tổng kết**:  
- **HDA** giúp tối ưu workflow, dễ dàng chia sẻ và cập nhật.  
- Sử dụng **hideWhen/disableWhen** để tạo giao diện thân thiện.  
- **Caching** và **Material Assignment** là bước quan trọng để tạo asset hoàn chỉnh.  

Chúc bạn thực hành thành công! 😊
