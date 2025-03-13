**GIÁO TRÌNH TUẤN 5: MÔ HÌNH THỦ TỤC (PROCEDURAL MODELING) TRONG HOUDINI**  
**Chủ đề:** Xây dựng thành phố procedural và tối ưu hóa cảnh  

---

### **Mục tiêu tuần học**  
- Hiểu cách tạo và quản lý cảnh phức tạp bằng kỹ thuật **instance**, **scattering**, và procedural setup.  
- Áp dụng dữ liệu OpenStreetMap (OSM) để xây dựng layout thành phố chân thực.  
- Tối ưu hóa hiệu suất render thông qua **packed primitives**, **delayed loading**, và **instancing**.  

---

### **Nội dung chi tiết**  

#### **1. Instantiation và Scattering**  
**Lý thuyết:**  
- **Instance**: Tạo nhiều bản sao từ một đối tượng gốc, giảm tải bộ nhớ và tăng tốc render.  
- **Scatter Node**: Phân bố điểm ngẫu nhiên trên bề mặt để đặt các instance.  
- **Kiểm soát mật độ**: Sử dụng **Paint Node** và **Attribute Noise** để điều chỉnh vùng tập trung điểm.  

**Thực hành:**  
- Tạo một tòa nhà đơn giản, sử dụng **Copy to Points** để sao chép instance.  
- Thêm **Scatter Node** kết hợp **Paint Node** để kiểm soát vị trí đặt các tòa nhà.  
- So sánh hiệu suất khi sử dụng **Packed Instance** vs. Unpacked Geometry.  

---

#### **2. Thiết lập Procedural cho Khu phố**  
**Lý thuyết:**  
- **Subdivision**: Chia lưới thành các khối nhỏ để tạo layout khu phố.  
- **Attribute Randomization**: Sử dụng VEX/Wrangle để thay đổi thuộc tính (chiều cao, vật liệu, cửa sổ) ngẫu nhiên.  

**Thực hành:**  
- Dùng **Labs Lot Subdivide** để chia lưới thành các ô đất.  
- Tạo vòng lặp **For-Each** để xây dựng từng tòa nhà với chiều cao và kiến trúc khác nhau.  
- Áp dụng **Attribute Randomize** để thay đổi vật liệu và kích thước cửa sổ.  

---

#### **3. Sử dụng Dữ liệu OpenStreetMap (OSM)**  
**Lý thuyết:**  
- **OSM Import Node**: Nhập dữ liệu địa lý từ OpenStreetMap vào Houdini.  
- **Lọc và làm sạch dữ liệu**: Xóa các phần thừa, tối ưu hình dạng công trình.  

**Thực hành:**  
- Tải file OSM từ [openstreetmap.org](https://www.openstreetmap.org), lọc lấy dữ liệu buildings và roads.  
- Dùng **Facet Node** và **Delete Node** để làm sạch hình dạng các tòa nhà.  
- Xuất dữ liệu thành Alembic để tái sử dụng.  

---

#### **4. Tạo Đường phố và Công trình Phụ trợ**  
**Lý thuyết:**  
- **Sweep Node**: Tạo độ dày cho đường phố từ đường cong.  
- **Boolean Node**: Cắt đường phố khỏi mặt đất để tạo độ chân thực.  

**Thực hành:**  
- Vẽ đường cong bằng **Draw Curve Node**, áp dụng **Sweep Node** để tạo đường.  
- Dùng **Boolean Node** kết hợp **Extrude** để tạo vỉa hè và lề đường.  
- Thêm đèn đường bằng **Copy to Points** kết hợp **Orient Attribute**.  

---

#### **5. Tối ưu hóa Cảnh**  
**Lý thuyết:**  
- **Packed Primitives**: Giảm tải bộ nhớ bằng cách lưu đối tượng dưới dạng tham chiếu.  
- **Delayed Loading**: Chỉ tải geometry khi cần thiết.  
- **Instancing trong Render**: Tối ưu cho Arnold/Mantra.  

**Thực hành:**  
- Chuyển đổi geometry thành **Packed Alembic**.  
- So sánh hiệu suất render khi sử dụng **Packed Instance** vs. Unpacked Geometry.  
- Áp dụng **Bounding Box Display** để giảm tải viewport.  

---

### **Bài tập cuối tuần**  
1. Tạo một khu phố procedural với ít nhất 3 biến thể kiến trúc khác nhau.  
2. Nhập dữ liệu OSM của một thành phố thực, xây dựng cảnh với đường phố và công trình.  
3. Render cảnh với **Packed Primitives** và so sánh thời gian/memory với phương pháp thông thường.  

---

### **Tài nguyên tham khảo**  
- **Houdini Documentation**: Nodes như *Copy to Points*, *Scatter*, *OSM Import*.  
- **OpenStreetMap**: Trích xuất dữ liệu địa lý miễn phí.  
- **Arnold/Mantra Settings**: Tối ưu render cho cảnh lớn.  

**Lưu ý:** Thử nghiệm nhiều phương pháp procedural khác nhau để tìm workflow phù hợp với dự án! 🌆
