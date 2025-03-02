### **Bắt đầu với Graph Neural Networks (GNNs) để sinh City Layout**  

GNNs rất phù hợp để tạo **city layout** vì hệ thống đường phố có thể biểu diễn dưới dạng **đồ thị (graph)**, trong đó:  
- **Node**: Giao lộ, điểm quan trọng trong thành phố.  
- **Edge**: Đường kết nối giữa các node.  

---

## **1. Xây dựng dữ liệu đầu vào cho GNNs**
### **(a) Lấy dữ liệu bản đồ từ OpenStreetMap (OSM)**
Dùng thư viện `osmnx` để tải dữ liệu đường phố dưới dạng graph:  
```python
import osmnx as ox
import networkx as nx

# Tải dữ liệu đường phố của một khu vực
city_name = "Tokyo, Japan"
G = ox.graph_from_place(city_name, network_type="all")

# Chuyển đồ thị thành định dạng NetworkX
G = ox.add_edge_lengths(G)
```
### **(b) Biến đổi dữ liệu để huấn luyện**
- **Node Features**: Loại giao lộ, mật độ đường.  
- **Edge Features**: Loại đường (cao tốc, phố nhỏ...), chiều dài, số làn xe.  
- **Graph Labels**: Quy hoạch thực tế của thành phố.  

---

## **2. Chọn mô hình GNNs**
Các mô hình phổ biến để huấn luyện **city layout**:  
- **Graph Convolutional Networks (GCN)**: Học từ mạng lưới đường.  
- **Graph Attention Networks (GAT)**: Tạo layout dựa trên trọng số ưu tiên.  

Ví dụ mô hình GCN dùng PyTorch Geometric:  
```python
import torch
import torch.nn.functional as F
from torch_geometric.nn import GCNConv

class CityLayoutGNN(torch.nn.Module):
    def __init__(self, in_channels, hidden_channels, out_channels):
        super(CityLayoutGNN, self).__init__()
        self.conv1 = GCNConv(in_channels, hidden_channels)
        self.conv2 = GCNConv(hidden_channels, out_channels)

    def forward(self, x, edge_index):
        x = self.conv1(x, edge_index)
        x = F.relu(x)
        x = self.conv2(x, edge_index)
        return x
```
- Input: **Graph (cấu trúc thành phố)**
- Output: **Graph mới (city layout đã tối ưu)**  

---

## **3. Huấn luyện mô hình**
- Chia tập dữ liệu: **80% training, 20% testing**  
- Dùng **Adam optimizer** và **Cross-Entropy Loss** để huấn luyện  
```python
optimizer = torch.optim.Adam(model.parameters(), lr=0.01, weight_decay=5e-4)

for epoch in range(200):
    optimizer.zero_grad()
    out = model(data.x, data.edge_index)
    loss = F.mse_loss(out, data.y)
    loss.backward()
    optimizer.step()
    print(f"Epoch {epoch}: Loss = {loss.item()}")
```

---

## **4. Xuất mô hình và tích hợp vào Houdini**
- Chuyển model sang **ONNX** để chạy inference trong Houdini  
```python
import torch.onnx

dummy_input = (data.x, data.edge_index)
torch.onnx.export(model, dummy_input, "city_layout.onnx")
```
- Dùng **Python SOP** để load model vào Houdini  
- Sinh đường phố procedural dựa trên AI output  

---

### 🚀 **Tiếp theo bạn muốn gì?**
1. **Viết script hoàn chỉnh để huấn luyện GNNs từ dữ liệu OSM?**
Dưới đây là **script hoàn chỉnh** để huấn luyện **GNNs** từ dữ liệu OpenStreetMap (OSM), dùng **PyTorch Geometric** để xử lý đồ thị.  

---

### **📌 Các bước chính:**
1. **Tải dữ liệu OSM** và chuyển thành đồ thị.  
2. **Xử lý dữ liệu** để tạo đặc trưng (features) cho node và edge.  
3. **Xây dựng mô hình GNN**.  
4. **Huấn luyện và kiểm tra mô hình**.  
5. **Xuất mô hình sang ONNX** để tích hợp vào Houdini.  

---

## **📌 Cài đặt thư viện cần thiết**
Trước khi chạy script, cần cài đặt các thư viện sau:  
```bash
pip install osmnx torch torch-geometric networkx numpy scikit-learn onnx
```

---

## **📌 Script huấn luyện GNNs từ dữ liệu OSM**
```python
import osmnx as ox
import networkx as nx
import torch
import torch.nn.functional as F
import torch_geometric
from torch_geometric.nn import GCNConv
from torch_geometric.data import Data
import numpy as np
from sklearn.preprocessing import StandardScaler

# 📌 1. TẢI DỮ LIỆU TỪ OPENSTREETMAP
city_name = "Tokyo, Japan"  # Bạn có thể đổi thành phố khác
G = ox.graph_from_place(city_name, network_type="drive")

# 📌 2. CHUYỂN ĐỔI ĐỒ THỊ SANG DỮ LIỆU PYTORCH GEOMETRIC
# Định danh node (vì OSM dùng ID rời rạc)
node_mapping = {node: i for i, node in enumerate(G.nodes)}
edge_index = []
node_features = []

# Duyệt từng node để lấy đặc trưng (ví dụ: tọa độ)
for node in G.nodes(data=True):
    lat, lon = node[1]["y"], node[1]["x"]  # Lấy tọa độ
    node_features.append([lat, lon])  # Có thể mở rộng feature nếu cần

# Chuẩn hóa node features
scaler = StandardScaler()
node_features = scaler.fit_transform(node_features)
node_features = torch.tensor(node_features, dtype=torch.float)

# Tạo danh sách cạnh (edges)
for u, v, _ in G.edges(data=True):
    edge_index.append([node_mapping[u], node_mapping[v]])

edge_index = torch.tensor(edge_index, dtype=torch.long).t().contiguous()

# Tạo graph data cho PyTorch Geometric
data = Data(x=node_features, edge_index=edge_index)

# 📌 3. ĐỊNH NGHĨA MÔ HÌNH GNN
class CityLayoutGNN(torch.nn.Module):
    def __init__(self, in_channels, hidden_channels, out_channels):
        super(CityLayoutGNN, self).__init__()
        self.conv1 = GCNConv(in_channels, hidden_channels)
        self.conv2 = GCNConv(hidden_channels, out_channels)

    def forward(self, x, edge_index):
        x = self.conv1(x, edge_index)
        x = F.relu(x)
        x = self.conv2(x, edge_index)
        return x

# Khởi tạo mô hình
in_channels = node_features.shape[1]
model = CityLayoutGNN(in_channels, 64, in_channels)

# 📌 4. HUẤN LUYỆN MÔ HÌNH
optimizer = torch.optim.Adam(model.parameters(), lr=0.01, weight_decay=5e-4)

for epoch in range(200):
    optimizer.zero_grad()
    out = model(data.x, data.edge_index)
    loss = F.mse_loss(out, data.x)  # Reconstruction loss
    loss.backward()
    optimizer.step()
    if epoch % 20 == 0:
        print(f"Epoch {epoch}: Loss = {loss.item()}")

# 📌 5. LƯU MÔ HÌNH VÀ CHUYỂN SANG ONNX
dummy_input = (data.x, data.edge_index)
torch.onnx.export(model, dummy_input, "city_layout.onnx")
print("Mô hình đã lưu thành công dưới dạng ONNX!")
```

---

## **📌 Giải thích script**
- **Tải dữ liệu từ OpenStreetMap (OSM)** và chuyển thành đồ thị NetworkX.  
- **Trích xuất đặc trưng node**: tọa độ `latitude` và `longitude`.  
- **Xây dựng GNN với 2 tầng Graph Convolutional Networks (GCN)**.  
- **Huấn luyện mô hình** để tái tạo layout thành phố.  
- **Xuất model ONNX** để inference trong Houdini.  

---

## **📌 Tiếp theo bạn muốn gì?**
1. **Chạy inference trong Houdini bằng Python SOP?**  
2. **Mở rộng mô hình với nhiều feature hơn (ví dụ: mật độ dân số, loại đường)?**  
3. **Tích hợp AI với PCG Graph trong Unreal Engine 5?** 🚀

