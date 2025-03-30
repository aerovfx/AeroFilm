Dưới đây là nội dung file đã được viết lại theo đúng trình tự procedural, với các bước rõ ràng từ khâu thiết lập địa hình đến xây dựng các phần của ngôi nhà, tạo tầng và mái, nhằm hướng dẫn làm cảnh phá hủy nhà trong Houdini.

---

# Procedural House – Chương Trình Làm Cảnh Phá Hủy Nhà Trong Houdini

## Mục tiêu
- **Giới thiệu quy trình:** Xây dựng một ngôi nhà theo phương pháp procedural, từ việc tạo địa hình (Terran Base) đến xây dựng các phần của ngôi nhà (tường, cửa, cột, mái) sử dụng các node trong Houdini.
- **Ứng dụng các kỹ thuật:** Sử dụng các node như geo, heightfield, poly extrude, attribute wrangle, group, blast, boolean… để tạo nên một mô hình có thể phá hủy được trong quy trình VFX.

---

## Phần 1: Level 1 – Cơ Bản

### Bước 1: Thiết Lập Terran Base (Địa Hình)
1. **Tạo Geo và Node Heightfield:**
   - Nhấn Tab trong Network View để tạo node geo đặt tên “Terran_base”.
   - Tạo node **heightfield** với thông số mặt phẳng ZX, kích thước 500×500 (diện tích đất).
2. **Tạo Hình Học Địa Hình & Ngọn Núi:**
   - Tạo node **Circle** với bán kính 100, chia 40 điểm để làm hình cơ sở của ngọn núi.
   - Thêm node **attribnoise** với thuộc tính P và biên độ (Amplitude) 50 để tạo nhiễu, sau đó dùng node **Smooth** làm mịn các cạnh.
   - Sử dụng node **Fuse** để gộp các điểm gần nhau (khoảng cách 0.001).
   - Dùng node **Polyfill** để lấp đầy hình dạng và node **Extrude** (khoảng cách = 1) để tạo độ dày cho hình học.
3. **Tạo Mask và Biến Đổi Heightfield:**
   - Project hình vừa tạo lên heightfield, đặt tên layer là “mask”.
   - Sử dụng node **Heightfield mask blur** để làm nhòe ranh giới mask.
   - Dùng node **Heightfield distort** với các tham số: Distortion Layer, Mask, Distort Amount, Frequency, Amplitude để tạo biến dạng tự nhiên.
   - Thêm node **Heightfield mask noise** nhằm tăng tính ngẫu nhiên cho mask.
4. **Vẽ Vị Trí Xây Nhà:**
   - Sử dụng node **Heightfield_paint** (với màu đỏ) để vẽ thủ công vùng xây nhà trên ngọn núi.

### Bước 2: Xuất Footprint Xây Nhà
- Sử dụng node **Heightfield scatter** để phân tán các điểm xây nhà dựa trên mask.
- Tạo node **null** đặt tên “OUT_BUILDING_FOOTPRINT” làm đầu ra cho phần footprint của ngôi nhà.

---

## Phần 2: Xây Dựng Ngôi Nhà (BUILDING)

### Bước 3: Tạo Geo BUILDING và Nhập Footprint
1. **Nhập Footprint:**
   - Nhấn Tab tạo geo mới có tên “BUILDING”.
   - Sử dụng node **object_merge** để load kết quả từ “OUT_BUILDING_FOOTPRINT”.
2. **Chuẩn Bị Hình Học:**
   - Sử dụng node **Unpack** để mở gói các đối tượng (packed primitives).
   - Dùng node **Divide** để chia nhỏ hình học, đồng thời chuyển UV bằng node **Transfer UV**.
   - Thêm node **Attribute Randomize** (cho thuộc tính như pscale, zscale) nhằm tạo tính ngẫu nhiên cho kích thước.

### Bước 4: Tạo Cửa và Cửa Sổ
- **Tạo đối tượng cơ bản:** Sử dụng node **Tube** cho cửa chính (door) và cửa sổ (windows).
- **Gán thuộc tính:** Dùng node **Attribute Wrangle** để gán biến nguyên (variant) với giá trị 0 cho door và 1 cho windows.
- **Merge và Điều Chỉnh:** Copy và gộp các đối tượng cửa, cửa sổ theo vị trí trung tâm được xác định từ footprint.

---

## Phần 3: Tạo Subnetwork “BOTTOM_FLOOR_WALLS”

### Bước 5: Tạo Subnetwork và Vòng Lặp Xử Lý
1. **Khởi tạo Subnetwork:**
   - Tạo một node (ví dụ: Tube), sau đó click vào biểu tượng màu vàng để chuyển thành subnetwork.
   - Đổi tên subnetwork thành **BOTTOM_FLOOR_WALLS** và double click vào để vào bên trong.
2. **Thiết lập Vòng Lặp:**
   - Tạo node **Block Begin Compile** và **Block End Compile** để tạo môi trường vòng lặp.
   - Thêm vòng lặp “For Each Piece” nhằm xử lý các mảnh (pieces) riêng lẻ.

### Bước 6: Xử Lý Các Nhánh Trong Subnetwork

#### Nhánh 1: Xây Dựng Cột Nhà (Corner Frames)
- **Lấy vị trí góc:** Tạo node **Null** đặt tên “cornerFrames” và tạo nhóm (group) “cornerFrames” để lấy vị trí các góc của khối nhà.
- **Loại bỏ phần thừa:** Sử dụng node **Dissolve** để loại bỏ các phần thừa.
- **Tạo cột:** Thêm node **Normal** (tính vector pháp tuyến) và sử dụng node **Sweep** để tạo hình trụ cho các cột.

#### Nhánh 2: Xác Định Vị Trí Cửa Chính & Cửa Sổ
- **Trích xuất điểm giữa:** Sử dụng node **Extract Centroid** để lấy tọa độ trung tâm của phần đối tượng, từ đó xác định vị trí cửa chính và cửa sổ.
- **Sắp xếp và nhóm:** Dùng node **Sort** để sắp xếp các điểm, sau đó tạo nhóm (Group) cho điểm cửa chính (door).
- **Tách nhóm:** Sử dụng node **Split** để chia các điểm thành 2 nhóm: door và windows.
- **Gán thuộc tính:** Dùng node **Attribute Wrangle** để gán:
  - `i@variant = 0;` cho cửa chính.
  - `i@variant = 1;` cho cửa sổ.
- **Merge:** Gộp các nhánh sau khi đã điều chỉnh vị trí và thuộc tính.

#### Nhánh 3: Xử Lý Khối Nhà Chính
- **Chia trục Y:** Sử dụng node **Divide** để chia nhỏ trục Y của khối nhà.
- **Đánh dấu nhóm:** Dùng node **Sort** và **Attribute Wrangle** với mã:
  ```
  if (@ptnum % ch("modula") == 0) {
      @group_offset = 1;
  }
  ```
  nhằm đánh dấu các điểm thuộc nhóm offset.
- **Xóa phần thừa:** Sử dụng node **Blast** để loại bỏ các mặt không cần thiết, giữ lại nhóm “offset”.
- **Tạo mảng tường:** Dùng node **Attribute Randomize** và **Polyextrude** để tạo các mảng tường dày, sau đó nhóm các mảng này thành nhóm “walls”.

### Bước 7: Gộp Các Nhánh và Tạo Khung Cửa (Frame)
- **Merge:** Gộp kết quả từ các nhánh 1, 2, 3.
- **Boolean:** Dùng node **Boolean** để xác định giao điểm giữa các khối (ví dụ: giữa các cột và mảng tường) nhằm tạo khung cho cửa.
- **Truyền thuộc tính:** Sử dụng node **Attribute Transfer** để chuyển thuộc tính variant (0 cho door, 1 cho windows).
- **Đầu ra khung:** Tạo node **Null** đặt tên “FRAME” làm khung cửa.
- **Tiếp tục xử lý:** Dùng node **Attribute Wrangle** khởi tạo các biến như group_door, group_windows. Làm sạch hình học của door và windows với các node: **Fuse**, **Facet**, **Normal**; sau đó dùng node **Split** và **Sweep** để hoàn thiện hình dạng. Cuối cùng, nhóm các phần này thành “doorFrames” và “windowFrames”.

### Bước 8: Hoàn Thành Subnetwork BOTTOM_FLOOR_WALLS
- **Kết hợp và làm sạch:** Merge tất cả các kết quả, xóa các thuộc tính và nhóm không cần thiết.
- **Đầu ra:** Thêm node đầu ra (Null) để hoàn thiện công việc của subnetwork.
- **Thoát Subnetwork:** Quay lại geo “BUILDING” và thêm node **Color**, cùng một node **Null** đặt tên “OUT_GROUND_FLOOR” để xác nhận kết quả tầng trệt.

---

## Phần 4: Xây Dựng Tầng 2 – TOP FLOOR

### Bước 9: Tạo Tầng 2
1. **Chuẩn bị hình học:**
   - Bắt đầu từ node **Unpack**.
   - Sử dụng node **Attribute Transfer** để truyền thuộc tính “class” và “building_id” từ tầng trệt.
   - Dùng node **Polyextrude** để tạo bề mặt của tầng 2, nhập khoảng cách từ đáy tầng 1 (dựa theo thông số từ node firstFloorHeight/dist).
2. **Nhóm và Subnetwork:**
   - Dùng node **Group Expression** để xác định các phần của tầng 2.
   - Tạo một subnetwork có tên **TOP_FLOOR_WALLS** (sao chép từ subnetwork BOTTOM_FLOOR_WALLS và đổi tên cho phù hợp).

---

## Phần 5: Tạo Mái Nhà (Roof)

### Bước 10: Tạo Subnetwork “ROOF_BASE”
1. **Vào Subnetwork Roof Base:**
   - Double click vào subnetwork, tạo các node **Fuse**, **Clean**, **Facet** để làm sạch hình học.
   - Thêm node **Rest Position** để lưu vị trí ban đầu của các điểm.
2. **Chuyển Sang Không Gian UV:**
   - Sử dụng node **Point Split** để tách các điểm dựa theo thuộc tính UV.
   - Dùng node **Attribute Wrangle** với mã:
     ```
     v@P = v@uv;
     @P.z = 0;
     ```
     nhằm chuyển các điểm sang mặt phẳng XY (trải phẳng geo lên UV).
3. **Tạo Kiểu Mái Nhà:**
   - Tạo node **Tube** để làm mái với 2 kiểu (ví dụ: kiểu 1 và kiểu 2) sử dụng node **Switch RoofType**.
   - Gom nhóm các phần mái với nhóm “mid”.
   - Dùng node **Attribute Wrangle** để đưa các điểm về vị trí ban đầu (lấy từ thuộc tính “rest”).
   - Áp dụng node **Polyextrude** để tạo hình cho mái.
4. **Đầu Ra Mái:**
   - Tạo 2 node **Null** đặt tên “OUT_ROOF_BASE” và “STEEL_ROOF_BASE”.
   - Sử dụng node **Group Expression** và **Blast** để xóa các nhóm không cần thiết, sau đó import roof base để bổ sung lớp tôn. Lặp lại (scale) để điều chỉnh kích thước mái tôn.

### Bước 11: Tạo Subnetwork “STEEL_ROOF”
- **Hoàn thiện mái tôn:** Tạo subnetwork STEEL_ROOF để hoàn thiện lớp tôn, merge mái tôn với sàn tôn theo yêu cầu.

---

## Phần 6: Hoàn Thiện Dự Án
1. **Làm Sạch Hình Học:**
   - Sử dụng node **Clean**, **AttribDelete** để xóa các thuộc tính và nhóm không cần thiết, đảm bảo geo gọn gàng.
2. **Xuất Kết Quả Cuối:**
   - Tạo các node đầu ra (Null nodes) cho từng phần: tầng trệt, tường, cửa, mái…
   - Merge tất cả các phần lại để hoàn thiện mô hình Procedural House cho cảnh phá hủy.

---

Qua quy trình trên, bạn đã xây dựng thành công một quy trình procedural từ khâu tạo địa hình, xây dựng các phần của ngôi nhà (bao gồm cả các chi tiết như cửa, cửa sổ, cột, tường) đến việc tạo tầng 2 và mái nhà trong Houdini. Quy trình này cho phép bạn tùy chỉnh, lặp lại và mở rộng nhằm phục vụ cho sản xuất VFX chuyên nghiệp.

Nếu có bất kỳ bước nào cần điều chỉnh hoặc bổ sung, bạn có thể tinh chỉnh lại các tham số và node theo yêu cầu cụ thể của dự án.

---
