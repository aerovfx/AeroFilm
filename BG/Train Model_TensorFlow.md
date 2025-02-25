# 🔷 Ví Dụ 2: Train Model với TensorFlow trong Houdini  

## **Bước 1: Cài đặt TensorFlow**  
Nếu chưa cài đặt TensorFlow, mở **Python Shell** trong Houdini và chạy:  

```python
import pip
pip.main(["install", "tensorflow"])
```

---

## **Bước 2: Tạo Python Script Node trong TOP**  
Tương tự như trên, tạo một **Python Script** node và thêm các tham số:  

- **epochs** (int, mặc định = 10)  
- **batch_size** (int, mặc định = 16)  
- **learning_rate** (float, mặc định = 0.001)  

Trong **Python Script**, dán đoạn code sau:  

```python
import tensorflow as tf
import numpy as np
import hou

# Lấy thông số từ Houdini
epochs = int(hou.pwd().parm("epochs").eval())
batch_size = int(hou.pwd().parm("batch_size").eval())
learning_rate = float(hou.pwd().parm("learning_rate").eval())

# Dummy dataset
x_train = np.random.randn(100, 1)
y_train = 3 * x_train + 2 + np.random.randn(100, 1) * 0.1

# Xây dựng model đơn giản
model = tf.keras.Sequential([
    tf.keras.layers.Dense(1, input_shape=(1,))
])

# Compile model
model.compile(optimizer=tf.keras.optimizers.Adam(learning_rate=learning_rate),
              loss='mse')

# Training
model.fit(x_train, y_train, epochs=epochs, batch_size=batch_size, verbose=1)

# Lưu model
model.save(hou.pwd().parm("outputfile").eval())
print("Model training complete and saved.")
```

---

## **Bước 3: Chạy Training**  
- Thêm tham số **outputfile** để lưu model (`output_model.h5`).  
- Nhấn **Cook Output Node** để chạy training.  
