# **PCA Reconstruction với Python**  

## **Giới thiệu**  
PCA (Principal Component Analysis) là một kỹ thuật giảm chiều dữ liệu phổ biến. PCA Reconstruction là quá trình khôi phục dữ liệu từ các thành phần chính sau khi đã giảm chiều.  

Ví dụ này minh họa việc áp dụng **PCA** trên tập dữ liệu **chữ số MNIST** (8x8 pixels), sau đó tái tạo lại ảnh từ dữ liệu đã giảm chiều.  

---

## **Các bước thực hiện**  

### **1. Load dữ liệu chữ số MNIST**  
- Sử dụng tập dữ liệu chữ số MNIST từ `sklearn.datasets.load_digits()`.  
- Mỗi ảnh có kích thước **8x8 pixels** (tổng cộng **64 chiều**).  

### **2. Áp dụng PCA để giảm chiều dữ liệu**  
- Sử dụng `PCA(n_components=20)` để giảm số chiều từ **64 xuống 20**.  
- Lưu lại dữ liệu đã giảm chiều để dùng cho tái tạo.  

### **3. Tái tạo lại ảnh từ dữ liệu PCA**  
- Dùng `inverse_transform()` để khôi phục ảnh từ dữ liệu đã giảm chiều.  

### **4. Hiển thị ảnh gốc và ảnh tái tạo**  
- So sánh ảnh gốc và ảnh tái tạo bằng **Matplotlib**.  

---

## **Mã nguồn đầy đủ**  
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.decomposition import PCA
from sklearn.datasets import load_digits

# Load dữ liệu chữ số MNIST (8x8 pixels)
digits = load_digits()
X = digits.data  # 1797 ảnh, mỗi ảnh có 64 pixels
y = digits.target  # Nhãn số tương ứng

# Hiển thị một vài ảnh gốc
fig, axes = plt.subplots(1, 5, figsize=(10, 3))
for i, ax in enumerate(axes):
    ax.imshow(X[i].reshape(8, 8), cmap='gray')
    ax.set_title(f'Label: {y[i]}')
    ax.axis('off')
plt.show()

# Giảm chiều bằng PCA (chỉ giữ lại 20 thành phần chính)
pca = PCA(n_components=20)
X_pca = pca.fit_transform(X)

# Tái tạo lại ảnh từ dữ liệu đã giảm chiều
X_reconstructed = pca.inverse_transform(X_pca)

# Hiển thị ảnh gốc và ảnh tái tạo để so sánh
fig, axes = plt.subplots(2, 5, figsize=(10, 6))

for i in range(5):
    # Ảnh gốc
    axes[0, i].imshow(X[i].reshape(8, 8), cmap='gray')
    axes[0, i].set_title(f'Original {y[i]}')
    axes[0, i].axis('off')

    # Ảnh tái tạo
    axes[1, i].imshow(X_reconstructed[i].reshape(8, 8), cmap='gray')
    axes[1, i].set_title(f'Reconstructed {y[i]}')
    axes[1, i].axis('off')

plt.show()


---

## **Kết quả mong đợi**  
- Ảnh **gốc** sẽ sắc nét.  
- Ảnh **tái tạo** có thể hơi mờ nhưng vẫn giữ được đặc trưng quan trọng của chữ số.  
- Nếu giảm `n_components`, ảnh tái tạo sẽ mất nhiều chi tiết hơn.  

Bạn có thể thử thay đổi giá trị `n_components` 
