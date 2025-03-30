### **📌 Tích hợp Procedural Modeling để cải thiện hình học thành phố trong Houdini**  

Sau khi đã tạo city layout bằng AI, bước tiếp theo là **tăng cường hình học** để tạo ra môi trường thực tế hơn. Điều này có thể được thực hiện bằng **Procedural Modeling** trong Houdini.  

---

## **📌 1️⃣ Mô hình hóa procedural với Freeway và Highway**
Mục tiêu:  
- **Tạo làn đường cho Freeway**  
- **Thêm vỉa hè và tòa nhà dọc theo Highway**  
- **Tự động đặt các khối nhà phù hợp với đường phố**  

### **🚀 A. Tạo Procedural Road System**
Dùng **Labs Road Generator** để tạo đường dựa trên dữ liệu inference:  

1. **Nhập city layout vào Houdini**  
   - Tạo Geometry Node (`city_roads`).  
   - Nhấn `Tab` và chọn **Labs Road Generator**.  
   - Kết nối với dữ liệu đường từ Python SOP.  

2. **Tăng độ chi tiết Freeway & Highway**  
   - Chỉnh **Lane Width** để mở rộng Freeway.  
   - Thêm **Divider Geometry** để tạo dải phân cách.  

---

### **🚀 B. Thêm Buildings bằng Procedural Blocks**
- Tạo Geometry Node (`city_buildings`).  
- Dùng **Labs Building Generator**:  
  - Nhập cạnh đường từ **city_roads**.  
  - Tự động tạo tòa nhà với chiều cao ngẫu nhiên.  
  - Chỉnh `Height Variance` để đa dạng hình dạng thành phố.  

---

## **📌 2️⃣ Kết hợp với AI để tối ưu bố cục thành phố**
- **Dùng AI để phân bổ mật độ nhà ở** dựa trên loại đường.  
- **Tự động sinh quảng trường hoặc khu công nghiệp** dựa trên node quan trọng.  
- **Dùng AI để điều chỉnh kích thước block phù hợp với giao thông.**  

---

## **📌 Tiếp theo
1. **Tích hợp AI + Procedural để sinh hoàn toàn một thành phố?**  
2. **Xuất dữ liệu Houdini sang Unreal Engine để render?** 🚀
