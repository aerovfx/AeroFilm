**Giáo Trình Tuần 2: Procedural Modeling cho Block Nhà trong Houdini**

---

## 1. Giới Thiệu
Trong bài giảng này, chúng ta sẽ tìm hiểu quy trình tạo một block nhà theo hướng procedural trong Houdini. Quá trình này giúp tự động hóa việc tạo các tòa nhà và block đồng bộ, nhanh chóng thay đổi cấu trúc khi cần thiết.

---

## 2. Quy Trình Xây Dựng Block Nhà

### 2.1. Chuẩn bị và thiết lập cơ bản
- **Tạo Geo Node**: Mở Houdini, tạo một Geometry Node mới (“block_building”).
- **Thiết lập Grid**: Dùng "Grid SOP" làm mặt đất cơ bản cho block nhà.
- **Tạo các Building Base**: Sử dụng "Copy to Points SOP" để phân bố đến các vị trí mong muốn.

### 2.2. Tạo nền móng và bố cục block nhà
- **Tạo base cho nhà**: Dùng "Box SOP" làm block nhà cơ bản.
- **Random height**: Dùng "Attribute Randomize SOP" để tạo độ cao ngẫu nhiên.
- **Biến đổi layout**: Kết hợp "Copy Stamp" hoặc "For Each Loop" để tạo biến thể.

### 2.3. Phát triển tường, cửa sổ và cửa ra vào
- **Tạo cửa sổ**: Dùng "Boolean SOP" để cắt hống trên tường.
- **Tạo pattern cửa sổ**: Dùng "Copy to Points" kèm theo ngẫu nhiên hoá vị trí.
- **Cửa ra vào**: Thêm "Boolean SOP" để tạo khoảng trống cho lối vào.

### 2.4. Thêm chi tiết kiến trúc
- **Ban công**: Tạo băng "Copy to Points" kèm "Grid SOP" làm lan can.
- **Mái hiên, cột**: Sử dụng "Tube SOP" hoặc "Line SOP" két hợp "Copy to Points".
- **Decor chi tiết**: Thêm đèn, cổng, thanh trang trí.

### 2.5. Tích hợp vật liệu và shading
- **Material SOP**: Thêm vật liệu chính cho nhà.
- **Texture VOP**: Mapping UV cho block nhà.
- **Randomize color**: Dùng "Attribute Randomize" cho màu sươn và tường.

### 2.6. Tối ưu hóa và xuất file
- **Clean Up Geometry**: Merge các Object thành "Packed Primitives".
- **Optimize Performance**: Giảm polycount bằng "Poly Reduce".
- **Xuất ra Engine khác**: Lưu dưới dạng FBX hoặc USD để dùng trong Unreal hoặc Unity.

---

## 3. Kết Luận
Với quy trình trên, chúng ta đã xây dựng hoàn chỉnh một block nhà procedural trong Houdini. Kỹ thuật này giúp giảm thiểu thời gian tạo mô hình và cho phép linh hoạt thay đổi thiết kế khi cần thiết.

---

### Bài tẬp
1. Thêm ngẫu nhiên hóa cho cửa sổ và cửa ra vào.
2. Tích hợp texture mô phỏng chất liệu bê tông, gỗ, kính.
3. Xuất block nhà ra Unreal Engine và đề xuất shading.

Hãy thực hành và tìm hiểu sâu hơn về procedural modeling trong Houdini!

