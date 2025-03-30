## **🎯 Hướng Dẫn Từng Bước Tích Hợp Ollama vào Houdini HDA Để Sinh 3D Model**  
Trong hướng dẫn này, bạn sẽ tạo một **Houdini Digital Asset (HDA)** có thể **gọi AI từ Ollama** để **sinh mô hình 3D** một cách tự động.  

---  

## **🔹 BƯỚC 1: Tạo Geometry Node Làm HDA**  
1️⃣ **Mở Houdini**, vào **/obj/**.  
2️⃣ **Nhấn Tab**, chọn **Geometry** → Đặt tên là `AI_Gen_Model`.  
3️⃣ Nhấn chuột phải vào node `AI_Gen_Model` → Chọn **Allow Editing of Contents**.  

---

## **🔹 BƯỚC 2: Thêm Python SOP Vào Geometry Network**  
1️⃣ **Double-click vào node `AI_Gen_Model`** để vào bên trong.  
2️⃣ **Nhấn Tab**, tìm **Python SOP** và đặt tên là `python_ai_gen`.  

📌 **Mẹo:**  
- Python SOP này sẽ gửi prompt đến AI và xử lý dữ liệu 3D từ AI.  
- Nó sẽ tạo mô hình dựa trên vertices (đỉnh) và faces (mặt).  

---

## **🔹 BƯỚC 3: Viết Code Python Trong Python SOP**  
1️⃣ Chọn `python_ai_gen`, nhìn xuống **Parameters Panel**.  
2️⃣ Tại phần **Python Code**, dán code sau:  

```python
import hou
import json
from ollama import Client

# Lấy tham số từ node HDA
parent_node = hou.pwd().parent()
use_ollama = parent_node.parm("use_ollama").eval()
ollama_host = parent_node.parm("ollama_host").eval()
prompt = parent_node.parm("prompt").eval()

# Kết nối AI Model
if use_ollama:
    llm = Client(host=ollama_host)
else:
    import llama_cpp
    llm = llama_cpp.Llama(model_path="path/to/your/model.gguf")

# Gửi Prompt cho AI để tạo Model
response = llm.generate(prompt)
mesh_data = json.loads(response['text'])  # Giả sử AI trả về JSON

# Truy cập Geometry của Houdini
geo = hou.pwd().geometry()

# Tạo các điểm (vertices)
points = {}
for i, v in enumerate(mesh_data['vertices']):
    point = geo.createPoint()
    point.setPosition(hou.Vector3(v[0], v[1], v[2]))
    points[i] = point

# Tạo các mặt (polygons)
for face in mesh_data['faces']:
    prim = geo.createPolygon()
    for vertex_id in face:
        prim.addVertex(points[vertex_id])
```

📌 **Lưu ý:**  
- `use_ollama`: Chọn **True** nếu dùng Ollama từ xa, **False** nếu chạy local.  
- `prompt`: Mô tả mô hình muốn tạo, ví dụ: `"Generate a futuristic car"`.  
- `ollama_host`: Địa chỉ của server Ollama nếu chạy trên máy khác.  

---

## **🔹 BƯỚC 4: Thêm Parameters Cho HDA**
1️⃣ **Chọn node `AI_Gen_Model`**, chuột phải → Chọn **Edit Parameter Interface**.  
2️⃣ **Kéo vào các tham số** sau từ tab **Create Parameters**:  
   - **Toggle** (Đặt tên `use_ollama`) → Để bật/tắt AI.  
   - **String** (Đặt tên `ollama_host`) → Nhập địa chỉ server Ollama.  
   - **String** (Đặt tên `prompt`) → Nhập mô tả model cần tạo.  
3️⃣ **Apply & Accept**.  

📌 **Mẹo:**  
- `use_ollama` giúp bật/tắt việc sử dụng AI.  
- `prompt` giúp thay đổi mô hình 3D chỉ bằng cách nhập text.  

---

## **🔹 BƯỚC 5: Biến Node Thành Houdini Digital Asset (HDA)**
1️⃣ **Chọn node `AI_Gen_Model`**, chuột phải → Chọn **Create Digital Asset...**.  
2️⃣ **Đặt tên file**, ví dụ: `"AI_Model_Generator.hda"`.  
3️⃣ **Chọn thư mục lưu**, rồi **OK**.  
4️⃣ Ở hộp thoại mới, nhấn **Accept** để lưu HDA.  

📌 **Lưu ý:**  
- HDA giúp lưu trữ tất cả logic AI vào một **node duy nhất**.  
- Bạn có thể tái sử dụng HDA này cho nhiều project khác nhau.  

---

## **🔹 BƯỚC 6: Sử Dụng HDA Để Sinh Model**
1️⃣ **Vào /obj/** → **Tab > AI_Model_Generator** (tìm HDA bạn vừa tạo).  
2️⃣ **Điền Prompt**, ví dụ: `"Generate a medieval castle with towers and walls"`.  
3️⃣ **Bật Display Flag** trên node.  
4️⃣ Houdini sẽ gọi **Ollama**, nhận dữ liệu, và vẽ mô hình 3D trong viewport! 🚀  

---

## **🎯 Kết Quả Mong Đợi*
✅ Houdini có thể tạo mô hình **procedural** từ AI
✅ Bạn có thể dễ dàng chỉnh sửa prompt để thay đổi mô hình.  
✅ Có thể mở rộng thêm **texturing, animation, hoặc AI traffic** trong Houdini! 🚀🔥
