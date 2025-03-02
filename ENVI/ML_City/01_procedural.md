
## **Nội dung chính của hướng dẫn**
### **1. Giới thiệu về PCG trong Unreal Engine 5**
- Unreal Engine 5 có một hệ thống **Procedural Content Generation (PCG)** mạnh mẽ giúp tạo nội dung môi trường một cách tự động, đặc biệt hữu ích cho thế giới mở.
- City Sample cho phép bạn sử dụng PCG để tạo các khu đô thị và đường cao tốc một cách nhanh chóng.

### **2. Cách thiết lập dự án**
- **Tải City Sample**: Trên Epic Games Launcher hoặc GitHub của Epic Games.
- **Import PCG Graph**: Chọn hệ thống PCG đã được thiết lập sẵn để tạo đường và tòa nhà.

### **3. Quy trình tạo thành phố và đường cao tốc**
- **PCG Graph cho thành phố**:
  - Tạo **lưới đường phố** dựa trên tập hợp quy tắc.
  - Xác định **khu vực xây dựng** bằng cách phân chia ô đất.
  - Tự động **spawn các tòa nhà** với vật liệu và chi tiết được tối ưu hóa.

- **PCG Graph cho đường cao tốc**:
  - Tạo **đường cao tốc liên kết** giữa các khu vực trong thành phố.
  - Thêm **đèn đường, lan can, biển báo giao thông**.
  - Định nghĩa quy tắc **cho xe cộ di chuyển tự động** (AI traffic).

### **4. Tinh chỉnh và tối ưu hóa**
- Dùng **HLOD (Hierarchical Level of Detail)** để tối ưu hiệu suất.
- Kiểm soát **density** của thành phố để phù hợp với phần cứng.
- Tinh chỉnh **collision** để tránh lỗi vật thể chồng lên nhau.

---

## **Ứng dụng thực tế**
- Dành cho **game thế giới mở** với thành phố rộng lớn.
- Hỗ trợ **simulations** như mô phỏng giao thông đô thị.
- Phù hợp cho các **dự án AR/VR**, đặc biệt là các ứng dụng bản đồ 3D.

