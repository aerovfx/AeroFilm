```markdown
# 🔥 Ví Dụ 1: Train Model với PyTorch trong Houdini  

## **Bước 1: Cài đặt PyTorch trong Houdini**  
Trước khi chạy, hãy đảm bảo Houdini có thể sử dụng PyTorch. Nếu bạn chưa cài đặt, mở **Python Shell** trong Houdini và chạy:  

```python
import pip
pip.main(["install", "torch", "torchvision"])
```

---

## **Bước 2: Tạo Python Script Node trong TOP**  
Trong Houdini, tạo một **TOP Network** (`Tab → TOP Network`).  

Thêm node **Python Script**, mở **Edit Parameter Interface** và tạo các tham số:  

- **epochs** (int, mặc định = 10)  
- **batch_size** (int, mặc định = 16)  
- **learning_rate** (float, mặc định = 0.001)  

Trong node **Python Script**, dán đoạn code sau:  

```python
import torch
import torch.nn as nn
import torch.optim as optim
from torch.utils.data import DataLoader, TensorDataset
import numpy as np

# Lấy thông số từ Houdini
epochs = int(hou.pwd().parm("epochs").eval())
batch_size = int(hou.pwd().parm("batch_size").eval())
learning_rate = float(hou.pwd().parm("learning_rate").eval())

# Dummy dataset: Tạo dữ liệu train ngẫu nhiên
x_train = torch.randn(100, 1)  # 100 điểm dữ liệu, 1 feature
y_train = 3 * x_train + 2 + torch.randn(100, 1) * 0.1  # y = 3x + 2 + noise

# Dataset loader
dataset = TensorDataset(x_train, y_train)
dataloader = DataLoader(dataset, batch_size=batch_size, shuffle=True)

# Định nghĩa model đơn giản
class LinearRegressionModel(nn.Module):
    def __init__(self):
        super(LinearRegressionModel, self).__init__()
        self.linear = nn.Linear(1, 1)

    def forward(self, x):
        return self.linear(x)

# Khởi tạo model
model = LinearRegressionModel()
criterion = nn.MSELoss()
optimizer = optim.Adam(model.parameters(), lr=learning_rate)

# Training loop
for epoch in range(epochs):
    for batch in dataloader:
        x_batch, y_batch = batch
        optimizer.zero_grad()
        y_pred = model(x_batch)
        loss = criterion(y_pred, y_batch)
        loss.backward()
        optimizer.step()
    
    if epoch % 2 == 0:
        print(f"Epoch {epoch}: Loss = {loss.item()}")

# Lưu model
torch.save(model.state_dict(), hou.pwd().parm("outputfile").eval())
print("Model training complete and saved.")
```

---

## **Bước 3: Chạy Training**  
- Thêm tham số **outputfile** vào node để lưu model (`output_model.pt`).  
- Nhấn **Cook Output Node** để chạy training.  
```
