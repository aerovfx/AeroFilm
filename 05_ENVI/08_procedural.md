*Giáo trình: Tạo cảnh quan CityCreationInHoudini bằng Procedural**
=====================================================================================

**Bước 1: Cài đặt và thiết lập môi trường**
------------------------------------------

*   **Khởi tạo Houdini**: Mở ứng dụng Houdini và chọn menu "File" > "New Scene" để tạo một file mới.
*   **Thiết lập cấu trúc thư mục**: Cài đặt thư mục cơ bản cho dự án, bao gồm cả thư mục data, script, assets v.v. Trong thư mục
`C:\DATA\ENVI\CityCreationInHoudini`, bạn sẽ có các thư mục sau:

    *   `data`: chứa các file dữ liệu (EX: shape, texture, mesh)
    *   `script`: chứa các file script Python (EX: procedural, logic)
    *   `assets`: chứa các file asset (EX: 3D model, texture)

**Bước 2: Tạo một vật thể cơ bản**
--------------------------------------

*   **Tạo một khối**: Chọn menu "Primitive" > "Cube" để tạo một khối.
*   **Thay đổi kích thước và vị trí**: Sử dụng thanh công cụ để thay đổi kích thước và vị trí của khối theo ý thích.

**Bước 3: Tạo hệ thống phân phối vật liệu**
---------------------------------------------

*   **Tạo một lớp phân phối**: Chọn menu "Layer" > "New Layer" để tạo một lớp phân phối mới.
*   **Thay đổi kích thước, vị trí và cường độ của lớp phân phối**: Sử dụng thanh công cụ để thay đổi kích thước, vị trí và cường độ của lớp phân
phối theo ý thích.

**Bước 4: Tạo hệ thống ánh sáng**
----------------------------------

*   **Tạo một nguồn ánh sáng mặt trời**: Chọn menu "Light" > "Sun" để tạo một nguồn ánh sáng mặt trời.
*   **Thay đổi vị trí, cường độ và màu sắc của nguồn ánh sáng**: Sử dụng thanh công cụ để thay đổi vị trí, cường độ và màu sắc của nguồn ánh sáng
theo ý thích.

**Bước 5: Tạo hệ thống hiệu ứng**
----------------------------------

*   **Tạo một hiệu ứng khói**: Chọn menu "Effects" > "Fog" để tạo một hiệu ứng khói.
*   **Thay đổi kích thước, vị trí và cường độ của hiệu ứng khói**: Sử dụng thanh công cụ để thay đổi kích thước, vị trí và cường độ của hiệu ứng
khói theo ý thích.

**Bước 6: Tạo một cảnh quan**
---------------------------

*   **Tạo một compositor mới**: Chọn menu "Compositor" > "New Composition" để bắt đầu tạo một cảnh quan.
*   **Thêm nhiều render khác nhau vào compositor**: Sử dụng thanh công cụ để thêm nhiều render khác nhau vào compositor để tạo một hình ảnh tổng
hợp.

**Bước 7: Xử lý và chỉnh sửa**
---------------------------------

*   **Sử dụng thanh công cụ để xử lý và chỉnh sửa**: Sử dụng thanh công cụ để xử lý và chỉnh sửa cảnh quan theo ý thích.
*   **Xuất file cuối cùng**: Xuất file cuối cùng của dự án.

**Ví dụ sử dụng procedural trong Houdini**
------------------------------------------

```python
# File procedural.py

import hou

# Tạo một khối mới
my_cube = hou.node("/obj/my_cube")

# Thay đổi kích thước và vị trí của khối
hou.setVector3d(my_cube.p, 100, 0, 10)

# Tạo một lớp phân phối mới
my_layer = hou.node("/layers/my_layer")

# Thay đổi kích thước, vị trí và cường độ của lớp phân phối
hou.setVector3d(my_layer.p, 50, 0, 5)
```

**Lưu ý**: Trong ví dụ trên, bạn có thể thay thế `hou` bằng cách sử dụng một thư viện khác như `pyhoudini`.
**Hướng Dẫn Chi Tiết: Tạo Compositing Ảnh Hưởng Sử dụng Blackmagic Design Fusion**

### Tạo Đỉnh Trời (Sky Dome)

Trước khi bắt đầu, bạn cần tạo một đỉnh trời (sky dome) để sử dụng trong compositing ảnh hưởng. Trong phần 
này, chúng ta sẽ sử dụng các công cụ và texture có sẵn trong Fusion để tạo ra đỉnh trời.

*   Tạo một hình vuông mới trong Fusion và đặt tên cho nó.
*   Sử dụng công cụ "Create" > "Plane" để tạo một mặt phẳng mới.
*   Đặt kích thước của mặt phẳng thành 2048x1024 pixel.
*   Sử dụng công cụ "Paint" để thêm màu sắc và texture vào đỉnh trời.

### Thêm mô hình 3D

Trong phần này, chúng ta sẽ thêm mô hình 3D từ Houdini vào Fusion và động nó trong thời gian thực.

*   Tải file mô hình 3D từ Houdini vào Fusion.
*   Sử dụng công cụ "Import" để nhập mô hình 3D vào Fusion.
*   Đặt vị trí và kích thước của mô hình 3D.

### Compositing

Compositing là quá trình kết hợp các lớp ảnh khác nhau lại với nhau để tạo ra một hình ảnh cuối cùng. Trong 
phần này, chúng ta sẽ thêm các lớp ảnh khác nhau vào compositing và điều chỉnh màu sắc và độ sáng.

*   Tạo một lớp mới trong Fusion và đặt tên cho nó.
*   Sử dụng công cụ "Import" để nhập lớp ảnh vào Fusion.
*   Đặt vị trí và kích thước của lớp ảnh.
*   Sử dụng công cụ "Color" để điều chỉnh màu sắc và độ sáng của lớp ảnh.

### Camera Matching

Camera matching là quá trình đồng bộ hóa camera của các cảnh quay khác nhau. Trong phần này, chúng ta sẽ sử 
dụng công cụ 3D của Fusion để đồng bộ hóa camera.

*   Tạo một hình vuông mới trong Fusion và đặt tên cho nó.
*   Sử dụng công cụ "Create" > "Camera" để tạo một camera mới.
*   Đặt vị trí và kích thước của camera.
*   Sử dụng công cụ "Transform" để điều chỉnh vị trí và kích thước của camera.

### Render

Cuối cùng, chúng ta sẽ render hình ảnh cuối cùng trong 32-bit floating-point format.

*   Tạo một hình vuông mới trong Fusion và đặt tên cho nó.
*   Sử dụng công cụ "Render" để render hình ảnh cuối cùng.
*   Đặt kích thước và chất lượng của hình ảnh.
*   Sử dụng công cụ "Save" để lưu hình ảnh cuối cùng.

Một số điểm cần chú ý khi sử dụng Fusion:

*   Hãy đảm bảo rằng bạn đã thiết lập không gian 3D đúng cách, bao gồm cả vị trí và kích thước của camera.
*   Sử dụng các công cụ có sẵn trong Fusion để tạo ra các hiệu ứng phức tạp như đỉnh trời và khói.
*   Compositing là một quá trình phức tạp và cần sự linh hoạt khi điều chỉnh màu sắc và độ sáng.
*   Hãy đảm bảo rằng bạn đã render hình ảnh cuối cùng trong 32-bit floating-point format để đạt được chất 
lượng hình ảnh tốt nhất.
