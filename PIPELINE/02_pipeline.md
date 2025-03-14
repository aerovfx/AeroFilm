Dưới đây là ví dụ minh hoạ một **pipeline** (quy trình) “phản chiếu” tham số HDA giữa **Houdini** và **Unreal Engine** bằng Python. Pipeline này có 3 phần chính:

1. **Trong Houdini**: Tạo Node + tham số, đóng gói thành HDA (bằng Python).  
2. **(Tuỳ chọn)** Xuất thông tin tham số ra tệp trung gian (JSON) để tiện quản lý hoặc kiểm tra.  
3. **Trong Unreal**: Dùng Python (hoặc Content Browser) để import HDA. Houdini Engine Plugin sẽ tự động hiển thị tham số trong Unreal.

> **Lưu ý quan trọng**:  
> - Phần code Python trong Houdini cần chạy **bên trong Houdini** (hoặc qua **Hython**).  
> - Phần code Python trong Unreal yêu cầu **Python Editor Script Plugin** (hoặc tương đương) được bật.  
> - Bạn cũng cần cài **Houdini Engine Plugin** cho Unreal để import và tương tác với HDA.

---

# 1. Tạo HDA và tham số trong Houdini

Dưới đây là một ví dụ Python chạy trong **Houdini** (Window > Python Shell, hoặc qua file `.py` trong Hython). Kịch bản:

- Tạo một **Geometry Node** ở `/obj`.  
- Thêm một vài tham số (translate, uniform scale, toggle, menu) bằng code.  
- Đóng gói node này thành một **HDA** (MyHDA.hda).

```python
import hou

# 1. Tạo một Geometry Node ở /obj
obj_context = hou.node("/obj")
geo_node = obj_context.createNode("geo", node_name="MyGeoNode", run_init_scripts=False)

# 2. Tạo một nhóm tham số (ParmTemplateGroup) và thêm tham số
parm_group = geo_node.parmTemplateGroup()

# a) Tham số Translate (3 giá trị: X, Y, Z)
translate_template = hou.FloatParmTemplate(
    name="translate",       # Tên nội bộ
    label="Translate",      # Tên hiển thị
    num_components=3,       # X, Y, Z
    default_value=(0.0, 0.0, 0.0),
    min=-100.0, max=100.0   # Ví dụ giới hạn
)
parm_group.append(translate_template)

# b) Tham số Uniform Scale (1 giá trị)
scale_template = hou.FloatParmTemplate(
    name="uniformscale",
    label="Uniform Scale",
    num_components=1,
    default_value=(1.0,),
    min=0.0, max=10.0
)
parm_group.append(scale_template)

# c) Tham số Difficulty (Menu)
diff_template = hou.MenuParmTemplate(
    name="difficulty",
    label="Difficulty",
    menu_items=["Easy", "Medium", "Hard"],
    menu_labels=["Easy", "Medium", "Hard"],
    default_value=1  # Mặc định là "Medium"
)
parm_group.append(diff_template)

# d) Tham số Add Shader? (Toggle)
shader_template = hou.ToggleParmTemplate(
    name="add_shader",
    label="Add Shader?",
    default_value=False
)
parm_group.append(shader_template)

# 3. Gán nhóm tham số mới vào node
geo_node.setParmTemplateGroup(parm_group)

# 4. Đóng gói thành HDA
hda_path = "/path/to/MyHDA.hda"  # Đường dẫn tệp HDA sẽ được tạo
new_hda = geo_node.createDigitalAsset(
    name="MyHDA",              # Tên asset
    hda_file_name=hda_path     # Đường dẫn file HDA
)

print(f"Đã tạo HDA tại: {hda_path}")
```

Sau khi chạy đoạn script này, bạn sẽ thấy một HDA mới tên “MyHDA” được lưu tại `MyHDA.hda`. Bên trong HDA, các tham số “Translate”, “Uniform Scale”, “Difficulty”, “Add Shader?” đã được định nghĩa.

---

# 2. (Tuỳ chọn) Xuất thông tin tham số ra JSON

Đoạn code sau **không bắt buộc** nhưng hữu ích nếu bạn muốn “phản chiếu” tham số sang các công cụ khác hoặc kiểm tra cấu trúc tham số. Nó đọc `ParmTemplateGroup` của node (hoặc HDA) rồi ghi ra file JSON.

```python
import hou
import json

# Giả sử node /obj/MyGeoNode hoặc một node HDA instance
node = hou.node("/obj/MyGeoNode")

parm_group = node.parmTemplateGroup().entriesWithoutFolders()
param_data = []

for t in parm_group:
    # Lấy kiểu tham số (Float, Menu, Toggle, v.v.)
    parm_type = t.type().name()
    # Nếu là Menu, có thể lấy danh sách item, v.v.
    
    param_info = {
        "name": t.name(),
        "label": t.label(),
        "type": parm_type
        # Có thể bổ sung "min", "max", "default", "menu_items", ...
    }
    param_data.append(param_info)

output_path = "/path/to/MyHDA_params.json"
with open(output_path, "w", encoding="utf-8") as f:
    json.dump(param_data, f, indent=4)

print(f"Đã ghi thông tin tham số ra {output_path}")
```

---

# 3. Import HDA vào Unreal Engine bằng Python

Để Unreal “nhận diện” tham số, bạn chỉ cần **import HDA** vào Unreal. Houdini Engine Plugin sẽ tự động hiển thị tham số trong chi tiết asset. Có 2 cách phổ biến:

1. **Dùng Content Browser** (thủ công):  
   - Mở Unreal, bật **Houdini Engine Plugin**.  
   - Trong Content Browser, chuột phải → Import to… → chọn file `MyHDA.hda`.  
   - Unreal sẽ tạo một asset Houdini, khi drag vào level, bạn sẽ thấy các tham số trong panel “Details”.

2. **Dùng Python Editor Script Plugin** (tự động):  
   Dưới đây là ví dụ code Python chạy trong Unreal (Editor) để import HDA:

   ```python
   import unreal

   # Tạo một AssetImportTask
   hda_import_task = unreal.AssetImportTask()
   hda_import_task.filename = r"C:\path\to\MyHDA.hda"        # Đường dẫn HDA
   hda_import_task.destination_path = "/Game/HoudiniAssets"  # Thư mục trong Content Browser
   hda_import_task.automated = True
   hda_import_task.save = True

   # Thực hiện import
   asset_tools = unreal.AssetToolsHelpers.get_asset_tools()
   asset_tools.import_asset_tasks([hda_import_task])

   # Kiểm tra asset vừa import
   imported_assets = hda_import_task.imported_object_paths
   print("Đã import các asset sau:", imported_assets)

   # (Tuỳ chọn) Tạo Actor trong Level
   # Lấy asset HDA
   if imported_assets:
       hda_path = imported_assets[0]  # Đường dẫn asset
       hda_asset = unreal.load_object(None, hda_path)
       
       # Tạo Actor trong Level
       actor_spawned = unreal.EditorLevelLibrary.spawn_actor_from_object(hda_asset, unreal.Vector(0,0,0))
       print("Actor mới:", actor_spawned)
   ```

Sau khi asset HDA được import, bạn có thể **drag** nó vào Level (hoặc spawn bằng script như trên). Khi chọn Actor đó, **Unreal** sẽ hiển thị các tham số (Translate, Uniform Scale, Difficulty, Add Shader,…) trong **Details Panel**. Thay đổi tham số → Houdini Engine sẽ “cook” lại HDA → cập nhật mesh/geometry trong Unreal.

---

## Tổng kết

- **Houdini**: Tạo Node + tham số → Đóng gói thành **HDA**.  
- **(Tuỳ chọn)**: Xuất thông tin tham số ra JSON (hoặc format khác) nếu muốn quản lý hay debug.  
- **Unreal**: Import HDA (thủ công hoặc bằng Python). Houdini Engine Plugin tự động hiển thị tham số.  

**Pipeline** này cho phép bạn **“phản chiếu”** (reflect) tham số HDA từ Houdini sang Unreal, giúp tạo và tùy chỉnh nội dung **procedural** trực tiếp bên Unreal Engine.  
