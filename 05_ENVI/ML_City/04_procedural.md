### **Chạy inference mô hình GNNs trong Houdini bằng Python SOP**  

Sau khi đã huấn luyện mô hình GNNs và lưu dưới dạng ONNX (`city_layout.onnx`), ta sẽ **tích hợp vào Houdini** để sinh city layout bằng **Python SOP**.  

---

## **📌 Các bước thực hiện**
1. **Tạo Python SOP trong Houdini**  
2. **Tải mô hình ONNX vào Houdini**  
3. **Chạy inference để tạo city layout**  
4. **Dùng Houdini để vẽ đường phố từ dữ liệu AI**  

---

### **1️⃣ Tạo Python SOP trong Houdini**
Mở **Houdini**, tạo **Geometry Node**, sau đó:  
- Thêm một **SOP** → Chọn **Python SOP**  
- Mở **Python Editor** và nhập đoạn script sau:  

---

### **2️⃣ Script Python SOP để chạy inference**
```python
import hou
import onnxruntime as ort
import numpy as np

# 📌 TẢI MÔ HÌNH ONNX
model_path = hou.evalParm("model_path")  # Tham số Houdini cho đường dẫn model
session = ort.InferenceSession(model_path, providers=["CPUExecutionProvider"])

# 📌 TẠO NODES TRONG HOUDINI
geo = hou.pwd().geometry()
geo.clear()  # Xóa dữ liệu cũ nếu có

# 📌 TẠO CÁC NODE ĐẦU VÀO
# Dữ liệu tọa độ nodes từ Houdini
node_positions = np.array([
    [hou.node("/obj/grid1").parm("tx").eval(), hou.node("/obj/grid1").parm("ty").eval()]
])  # Lấy vị trí của node (Ví dụ)

edge_index = np.array([
    [0, 1], [1, 2]  # Giả lập danh sách cạnh nối các điểm
])

# Chuyển đổi sang Tensor ONNX
node_positions = np.float32(node_positions)
edge_index = np.int64(edge_index)

# 📌 CHẠY INFERENCE
outputs = session.run(None, {"x": node_positions, "edge_index": edge_index})

# 📌 DỰNG ĐƯỜNG PHỐ TRONG HOUDINI
for i, pos in enumerate(outputs[0]):  
    p = geo.createPoint()
    p.setPosition(hou.Vector3(pos[0], pos[1], 0))  # Đặt node lên viewport Houdini

# Kết nối các node bằng cạnh
for edge in edge_index:
    poly = geo.createPolygon()
    poly.addVertex(geo.iterPoints()[edge[0]])
    poly.addVertex(geo.iterPoints()[edge[1]])
```

---

## **📌 Hướng dẫn chi tiết**
1. **Tạo Geometry Node** trong Houdini.  
2. **Thêm Python SOP** vào node và nhập script trên.  
3. **Chỉnh tham số model_path** → Trỏ đến file `city_layout.onnx`.  
4. **Chạy Houdini** để thấy **đường phố được tạo từ AI**! 🚀  

---
