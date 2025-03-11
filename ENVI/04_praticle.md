**Giáo Trình Tuần 4: Xây Dựng Cảnh Thành Phố Procedural trong Houdini**  
*Chủ đề: Tạo cảnh quan tổng thể, tích hợp địa hình, thiết lập camera và layout*

---

### **Phần 1: Giới Thiệu Tổng Quan**
**Mục tiêu:**  
- Hiểu cách xây dựng cảnh thành phố procedural từ địa hình đến bố cục.  
- Làm chủ workflow kết hợp giữa Houdini và Gaia để tạo địa hình phức tạp.  
- Thiết lập camera và chuyển động để tăng tính điện ảnh cho cảnh.

---

### **Phần 2: Tạo Địa hình với Houdini và Gaia**  
#### **2.1. Sử dụng Height Fields trong Houdini**  
- **Công cụ:** Node `Height Field Noise`, `Erosion`, `Mask by Slope`.  
- **Công thức cơ bản:**  
  ```python
  # Tạo nhiễu cho địa hình
  height = noise(pos * frequency) * amplitude
  ```
- **Ví dụ:**  
  - Tạo núi: Sử dụng `Height Field Noise` với kiểu *Sparse Convolution*.  
  - Thêm sông: Dùng `Erosion` điều chỉnh `Downcutting` và `Sediment`.  

#### **2.2. Tích hợp Gaia cho địa hình chi tiết**  
- **Bước 1:** Xuất height map từ Houdini sang Gaia (định dạng `.tiff`).  
- **Bước 2:** Trong Gaia:  
  - Dùng node **Canyon** để tạo khe núi.  
  - Thêm **Snowfall** và **River** để tạo hiệu ứng tự nhiên.  
- **Lưu ý:** Sử dụng **Portals** để kết nối dữ liệu giữa các graph trong Gaia.

---

### **Phần 3: Thiết Lập Layout và Proxy Geometry**  
#### **3.1. Tạo Proxy Buildings**  
- **Công cụ:** Node `L-System`, `Copy to Points`.  
- **Ví dụ:**  
  ```python
  // L-System rule để tạo tòa nhà
  rule: A → F(10)[+A][-A] // Tạo nhánh ngẫu nhiên
  ```
- **Ứng dụng:** Phân bố các khối hộp ngẫu nhiên dựa trên điểm phân tán (scatter points).

#### **3.2. Thêm Sông và Hồ**  
- **Công cụ:** Node `Curve`, `PolyExtrude`.  
- **Thủ thuật:** Dùng `Attribute Wrangle` để điều khiển độ sâu sông:  
  ```python
  @depth = fit01(rand(@ptnum), 5, 15); // Độ sâu ngẫu nhiên từ 5-15m
  ```

---

### **Phần 4: Thiết Lập Camera và Composition**  
#### **4.1. Quy tắc bố cục**  
- **Quy tắc 1/3:** Đặt điểm nhấn (ví dụ: tòa nhà chính) tại giao điểm của các đường 1/3.  
- **Ví dụ:** Camera di chuyển từ góc dưới phải lên góc trên trái, tập trung vào tòa nhà trung tâm.

#### **4.2. Tạo Chuyển Động Camera**  
- **Bước 1:** Đặt keyframe cho vị trí và góc quay.  
- **Bước 2:** Mở **Animation Editor** để điều chỉnh bezier curve:  
  - Tăng tốc đầu (ease-in) và giảm tốc cuối (ease-out).  
- **Công thức:**  
  ```python
  // Tính toán chuyển động mượt
  position = lerp(start_pos, end_pos, smoothstep(0, 1, t))
  ```

---

### **Phần 5: Xuất Cảnh và Tích Hợp**  
#### **5.1. Xuất Alembic từ Houdini**  
- **Công cụ:** Node `Alembic Export`.  
- **Cài đặt:** Chọn *Geometry* và *Materials* để giữ nguyên thông số shader.  

#### **5.2. Tích Hợp Với Render Engine**  
- **Mẹo:** Dùng `Redshift` hoặc `Karma` để render cảnh:  
  - Áp dụng **Atmospheric Perspective** để tạo chiều sâu.  
  - Thêm **Volumetric Fog** cho hiệu ứng sương mù.

---

### **Bài Tập Thực Hành**  
1. Tạo dãy núi trong Houdini với `Height Field Erosion`, xuất sang Gaia để thêm sông.  
2. Dùng `L-System` sinh 50 tòa nhà proxy và phân bố ngẫu nhiên.  
3. Thiết lập camera di chuyển từ cận cảnh tòa nhà ra toàn cảnh thành phố (24 frames).

---

### **Tổng Kết**  
- **Địa hình:** Kết hợp Houdini và Gaia để tạo địa hình tự nhiên.  
- **Layout:** Sử dụng proxy geometry để dựng cảnh nhanh.  
- **Camera:** Áp dụng quy tắc 1/3 và chuyển động mượt để tăng tính điện ảnh.  

