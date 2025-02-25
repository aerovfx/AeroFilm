# Hướng Dẫn Tạo HDA Cho TOP Network Trong Houdini

## **Bước 1: Tạo Mạng Lưới TOP (PDG)**
1. **Tạo một TOP Network**  
   - Trong **/obj** hoặc **/stage**, nhấn `Tab → TOP Network`.  
   - Hoặc trong SOPs, sử dụng `Tab → TOP Geometry`.  

2. **Thêm các node cần thiết**  
   - Ví dụ:
     - `TOP Fetch` (Lấy dữ liệu từ SOPs)
     - `ROP Geometry Output` (Xuất geometry từ PDG)
     - `Wait for All` (Đồng bộ task)
     - `Python Script` (Chạy script tùy chỉnh)
     - `MQTT Publish` (Gửi kết quả đến AI hoặc ML)
     - `Generic Generator` (Tạo tác vụ tùy chỉnh)

3. **Kiểm tra mạng lưới**  
   - Nhấn **Cook Output Node** để chạy thử PDG.

---

## **Bước 2: Chuyển Thành HDA**
4. **Đóng gói thành HDA**  
   - Chọn tất cả node TOP.
   - Nhấn `Shift + C` để tạo **Subnet**.
   - Click chuột phải vào Subnet **→ Create Digital Asset**.
   - Đặt tên, ví dụ: `ML_Terrain_TOP.hda`.

5. **Thiết lập Parameters**  
   - Mở **Type Properties** của HDA.
   - Promote các tham số quan trọng từ các node bên trong (ví dụ: input file, output path, AI model selection…).

6. **Lưu và Kiểm tra**  
   - Nhấn **Save Node Type**.
   - Tạo một TOP Network mới, kéo HDA vào để kiểm tra.

---

## **Bước 3: Chia Sẻ Hoặc Sử Dụng Lại**
- Xuất `.hda` và load trên máy khác qua **Asset Manager → Install Asset Library**.
- Nếu update HDA, chỉnh sửa **Type Properties**, nhấn **Save Node Type**, chọn **Match Current Definition**.

---


