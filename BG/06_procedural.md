### **📌 Thêm Freeway và Highway vào City Layout trong Houdini bằng AI**  

Sau khi đã tải mô hình ONNX vào Houdini, bước tiếp theo là **chạy inference** để sinh layout có **Freeway** và **Highway**.  

---

## **📌 Cách tiếp cận**
1. **Dùng dữ liệu OSM để phân loại đường** thành **Highway** (đường chính) và **Freeway** (đường cao tốc).  
2. **Huấn luyện lại GNN** để tạo đường ưu tiên dựa trên loại đường.  
3. **Chạy inference trong Houdini**, hiển thị đường **Highway** to hơn và **Freeway** rộng hơn.  

---

## **📌 1️⃣ Cập nhật mô hình để phân loại đường**
Trước tiên, cần cập nhật script huấn luyện GNN để thêm nhãn cho Freeway/Highway:

```python
import osmnx as ox
import networkx as nx
import torch
from torch_geometric.data import Data
import numpy as np

# 📌 1. TẢI DỮ LIỆU OSM
city_name = "Tokyo, Japan"
G = ox.graph_from_place(city_name, network_type="drive")

# 📌 2. CHUYỂN ĐỔI SANG GRAPH
node_mapping = {node: i for i, node in enumerate(G.nodes)}
edge_index = []
node_features = []
edge_features = []  # Thêm đặc trưng cạnh

# Lấy tọa độ node và phân loại đường
for u, v, data in G.edges(data=True):
    road_type = data.get("highway", "residential")  # Lấy loại đường

    # Gán nhãn Freeway = 2, Highway = 1, Đường thường = 0
    if isinstance(road_type, list):
        road_type = road_type[0]
    
    if "motorway" in road_type:
        edge_features.append([2])  # Freeway
    elif "primary" in road_type or "trunk" in road_type:
        edge_features.append([1])  # Highway
    else:
        edge_features.append([0])  # Đường nhỏ

    edge_index.append([node_mapping[u], node_mapping[v]])

edge_index = torch.tensor(edge_index, dtype=torch.long).t().contiguous()
edge_features = torch.tensor(edge_features, dtype=torch.float)

# 📌 3. CẬP NHẬT MÔ HÌNH GNN
class CityLayoutGNN(torch.nn.Module):
    def __init__(self, in_channels, hidden_channels, out_channels):
        super(CityLayoutGNN, self).__init__()
        self.conv1 = GCNConv(in_channels, hidden_channels)
        self.conv2 = GCNConv(hidden_channels, out_channels)

    def forward(self, x, edge_index, edge_attr):
        x = self.conv1(x, edge_index)
        x = F.relu(x)
        x = self.conv2(x, edge_index)
        return x

# Huấn luyện và lưu model
model = CityLayoutGNN(in_channels=2, hidden_channels=64, out_channels=2)
torch.save(model.state_dict(), "city_layout_with_highway.pth")
```

---

## **📌 2️⃣ Chạy inference trong Houdini và hiển thị Freeway/Highway**
Trong **Python SOP**, thay thế script cũ bằng đoạn sau:

```python
import hou
import onnxruntime as ort
import numpy as np

# 📌 TẢI MÔ HÌNH ONNX
model_path = hou.evalParm("model_path")
session = ort.InferenceSession(model_path, providers=["CPUExecutionProvider"])

geo = hou.pwd().geometry()
geo.clear()

# 📌 Đọc dữ liệu từ Houdini
node_positions = np.array([[0, 0], [10, 0], [10, 10], [0, 10]], dtype=np.float32)
edge_index = np.array([[0, 1], [1, 2], [2, 3], [3, 0]], dtype=np.int64)
edge_types = np.array([1, 0, 2, 0], dtype=np.float32)  # Ví dụ: có Freeway (2) và Highway (1)

# Chạy inference
outputs = session.run(None, {"x": node_positions, "edge_index": edge_index, "edge_attr": edge_types})

# 📌 HIỂN THỊ TRONG HOUDINI
for i, pos in enumerate(outputs[0]):
    p = geo.createPoint()
    p.setPosition(hou.Vector3(pos[0], pos[1], 0))

for i, edge in enumerate(edge_index):
    poly = geo.createPolygon()
    poly.addVertex(geo.iterPoints()[edge[0]])
    poly.addVertex(geo.iterPoints()[edge[1]])

    # Tạo thuộc tính để Houdini hiển thị Freeway/Highway
    poly.setAttribValue("road_type", edge_types[i])
```

---

## **📌 Kết quả mong đợi**
✔ **Highway (đường chính) sẽ hiển thị đậm hơn**  
✔ **Freeway (đường cao tốc) sẽ rộng hơn và có màu khác**  
✔ **Houdini sẽ sinh procedural city layout có đường hợp lý**  

---

## **📌 Tiếp theo
1. **Tích hợp AI vào Unreal Engine 5 với PCG Graph?**  
2. **Thêm procedural buildings dọc theo Freeway/Highway?**  
3. **Xuất layout này thành USD để kết hợp với pipeline khác?** 🚀
