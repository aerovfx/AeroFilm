---

## 🟤 **1. Cylinder – Workflow Cơ Bản với Smart Material**

### Các bước:

1. **Block màu cơ bản**:

   * Tạo từng Fill Layer cho từng phần chất liệu (kim loại, nhựa, v.v.).
   * Dùng Mask để phân chia các vùng.
   * Mục đích: Đẩy nhanh phần “việc nhàm chán” ban đầu.

2. **Áp dụng Smart Material**:

   * Chọn Smart Material phù hợp, gán vào từng vùng.
   * Điều chỉnh nhanh các thông số: Roughness, Color, Height,...
   * Không cần làm quá chi tiết ở giai đoạn này.

3. **Tạo Preset cho vật liệu đơn giản**:

   * Ví dụ: Kim loại đơn giản (buckle), không cần đầu tư nhiều thời gian.
   * Tạo một Smart Material từ preset có sẵn → gán và chỉnh lại màu & độ bóng.

4. **Tối ưu thời gian**:

   * Không cần "mài giũa" từng vật liệu quá kỹ.
   * Sử dụng lại Smart Materials, chỉnh nhanh trên Layer Stack.
   * Thời gian lý tưởng cho một vật liệu: dưới 10 phút.

### 💡Tips:

* Đối với chi tiết nhỏ không quan trọng: tạo preset riêng để gán nhanh.
* Tập trung vào vùng nổi bật thay vì từng pixel.
* Dùng **HSL Adjustment Layer** để điều chỉnh toàn bộ màu sau cùng trước khi xuất file.

---

## 🟠 **2. Belt\_Model – Tinh chỉnh bằng AO và Generators**

### Các bước:

1. **Sử dụng Generator**:

   * Áp dụng các hiệu ứng như Dirt, Edge Wear.
   * Dựa trên Ambient Occlusion, Curvature map để tăng độ chân thật.
   * Có thể thêm **Grunge Map** để tăng độ phức tạp.

2. **Mask nâng cao**:

   * Dùng Black Mask + Generator để điều khiển mức độ ảnh hưởng.
   * Tùy chỉnh thông số như Balance, Contrast, Dirt Level, để đạt độ chân thật mong muốn.

3. **Làm sạch các cạnh sắc**:

   * Dùng Paint Tool trong Mask để xóa bớt hiệu ứng ở các vùng không mong muốn.

4. **Gán chi tiết micro bằng Normal Map**:

   * Tạo các hiệu ứng như vết xước nhỏ, khắc logo, bằng cách thêm Layer ảnh vào kênh Normal.
   * Sử dụng chế độ **Normal Combine** và điều chỉnh độ mạnh.

### 💡Tips:

* Dùng Fill Layer + Black Mask để kiểm soát từng lớp chất liệu.
* Tạo nhóm riêng cho từng vật liệu để dễ quản lý.
* Tăng độ chân thật bằng các Layer “damage” nhỏ (vết mòn, bụi...).

---

## 🟣 **3. Pilot\_Helmet – Chuẩn bị Render & Engine**

### Các bước:

1. **Final Touch trong Substance Painter**:

   * Thêm Layer điều chỉnh HSL để cân chỉnh màu sắc phù hợp với môi trường Engine (Unreal, Marmoset).
   * Tạo một folder “Engine Adjustments”, đặt HSL và Roughness adjustment trong đó.
   * Set các layer này thành “Pass Through” và “Affect All Channels”.

2. **Xuất sang Engine**:

   * Export textures với cấu hình phù hợp (Metallic/Roughness hoặc Specular workflow).
   * Import vào Unreal Engine / Marmoset và kiểm tra lại ánh sáng & chất liệu.

3. **Điều chỉnh lại trong Engine**:

   * Trong Unreal hoặc Marmoset, nếu chất liệu quá bóng hoặc quá tối, quay lại Substance và chỉnh trong Layer “Engine Adjustments”.

4. **Kiểm tra với Lighting khác nhau**:

   * Dùng HDRi hoặc Lighting Studio khác nhau để test phản xạ và màu.
   * Ưu tiên giữ môi trường trung tính như **Tomoko** để dễ đánh giá.

### 💡Tips:

* Nên có 1 layer màu điều chỉnh tổng thể sau cùng (Color Fix).
* Có thể tăng hoặc giảm độ bóng toàn scene chỉ bằng 1 slider.
* Tránh chỉnh lighting quá nhiều trong Painter – hãy làm điều đó trong Engine.

---

