### **📌 Bước 1: Tạo Python SOP trong Houdini**  

#### **1. Mở Houdini và tạo Geometry Node**  
- Mở Houdini và vào **Network Editor**.  
- Trong **/obj**, tạo một **Geometry Node** (Ctrl + Click vào Geometry).  
- Đổi tên node thành **city_layout** (hoặc tên bạn muốn).  

#### **2. Thêm Python SOP**  
- Trong **Geometry Node**, nhấn **Tab** và tìm **Python SOP**.  
- Kết nối Python SOP vào node Geometry.  
- Chọn Python SOP và mở **Parameter Editor**.  

---

### **📌 Bước 2: Tải mô hình ONNX vào Houdini**  

#### **1. Cài đặt thư viện ONNX Runtime nếu chưa có**  
Houdini sử dụng Python tích hợp sẵn, nhưng bạn có thể cần cài ONNX Runtime thủ công:  
```bash
pip install onnxruntime
```
Nếu Python của Houdini không có pip, bạn có thể tìm đường dẫn **Houdini Python** (`hython`) để cài đặt.

#### **2. Tạo Parameter để chọn mô hình ONNX**
- Trong Python SOP, nhấn **Gear Icon** (góc phải trên) → Chọn **Edit Parameter Interface**.  
- Nhấn **+ String Parameter**, đặt tên là `model_path`.  
- Chọn **Browse File** và trỏ đến file `city_layout.onnx`.  
- Nhấn **Accept**.  

#### **3. Viết script để load mô hình ONNX**
Trong **Python SOP**, mở **Python Editor** (Alt + E) và nhập:  

```python
import hou
import onnxruntime as ort

# 📌 Lấy đường dẫn mô hình từ Houdini Parameter
model_path = hou.pwd().evalParm("model_path")

# 📌 Kiểm tra file ONNX có tồn tại không
if not model_path:
    raise ValueError("Chưa chọn file ONNX!")

# 📌 Tải mô hình ONNX
try:
    session = ort.InferenceSession(model_path, providers=["CPUExecutionProvider"])
    print(f"✅ Đã load model ONNX: {model_path}")
except Exception as e:
    print(f"⚠️ Lỗi khi load model: {e}")
```
---

## ✅ **Kết quả sau bước 1 và 2**  
✔ **Geometry Node "city_layout" đã có Python SOP.**  
✔ **ONNX Model được chọn và load thành công vào Houdini.**  

---

### **📌 Tiếp theo bạn muốn làm gì?**
1. **Chạy inference để sinh city layout trong Houdini?**  
2. **Hiển thị điểm và kết nối bằng edges để tạo đường phố?** 🚀
