### **Bước 1 - Thiết lập dự án Houdini cần thiết**  

Trước khi bạn có thể sử dụng Houdini để tạo thành phố, bạn cần thiết lập một số thứ trên máy tính, bao gồm việc giải nén các tệp nguồn cần thiết để hoàn thành hướng dẫn này. Bạn cũng cần xác định và tạo một số thư mục để lưu trữ dữ liệu cho thành phố của mình, những thư mục này sẽ được sử dụng trong các bước sau.  

Trong thư mục gốc nơi lưu dự án **City Sample**, hãy tìm tệp **CitySample_HoudiniFiles.zip**. Đây là tệp chứa các tệp nguồn của Houdini cần thiết để hoàn thành hướng dẫn này.
![image](https://github.com/user-attachments/assets/a797c415-15f5-4993-87a7-284cc15c3e47)
### **Tạo thư mục để lưu tệp nguồn**  

1. **Tạo một thư mục mới** để lưu các tệp nguồn. Trong hướng dẫn này, vị trí lưu trữ mặc định được sử dụng là:  
   ```
   D:\CitySampleSource
   ```
   Hướng dẫn sẽ giả định rằng bạn đang sử dụng một thư mục có tên và vị trí tương tự.  

2. **Giải nén tệp** `CitySample_HoudiniFiles.zip` vào thư mục vừa tạo.  

3. Sau khi giải nén, một thư mục có tên **Small_City** sẽ xuất hiện. Đường dẫn đến thư mục này sẽ trông như sau:  
   ```
   D:\CitySampleSource\Small_City
   ```
   ![image](https://github.com/user-attachments/assets/7540c930-deb6-425a-b161-9432905456a6)
### **Mở tệp cấu hình `houdini.env` trên Windows**  

1. Điều hướng đến thư mục **Documents** trên hệ thống Windows của bạn:  
   ```
   C:\Users\{your_user_name}\Documents\houdini18.5
   ```
   (Thay `{your_user_name}` bằng tên người dùng của bạn trên máy tính.)  

2. Tìm tệp có tên **`houdini.env`**.  

3. **Mở tệp này bằng một trình soạn thảo văn bản**, chẳng hạn như:  
   - **Notepad** (mặc định của Windows)  
   - **Notepad++** (khuyến nghị)  
   - **Visual Studio Code** (nếu bạn muốn định dạng dễ đọc hơn)  
![image](https://github.com/user-attachments/assets/a8c01e61-91f6-4c40-995a-0e0900f3add9)

### **Chỉnh sửa tệp `houdini.env` để tích hợp City Sample**  

1. **Mở tệp `houdini.env`** theo hướng dẫn trước.  

2. **Thêm dòng sau vào cuối tệp:**  
   ```plaintext
   HOUDINI_PATH = D:/CitySampleSource/Small_City/houdini;&
   ```
   Nếu dòng này đã có sẵn, hãy đảm bảo không có lỗi cú pháp.  

3. **Lưu lại tệp `houdini.env`** và đóng trình soạn thảo.  

💡 **Lưu ý:**  
- **Dấu `;&`** ở cuối dòng giúp Houdini giữ nguyên các đường dẫn mặc định và chỉ thêm đường dẫn mới.  
- Nếu bạn sử dụng nhiều phiên bản Houdini, hãy kiểm tra lại thư mục `houdini18.5` để đảm bảo đúng phiên bản.  
![image](https://github.com/user-attachments/assets/c0865d04-ccf2-4963-b7c9-a54f8f64acd1)

### **Xác minh cài đặt Houdini cho City Sample**  

1. **Lưu tệp `houdini.env`** sau khi đã thêm đường dẫn.  

2. **Khởi động Houdini** như bình thường.  

3. **Kiểm tra danh sách Houdini Digital Assets (HDA):**  
   - Từ menu chính, chọn **Asset > Asset Manager**.  
   - Trong **Asset Manager**, mở rộng mục **Operator Type Libraries > Scanned Asset Library Directories**.  
   - Cuộn xuống cuối danh sách để tìm các tệp **`.hda`**, đảm bảo rằng chúng đã được tải từ thư mục mà bạn đã thêm trong `houdini.env`.  

✅ **Nếu các tệp `.hda` xuất hiện**, điều đó có nghĩa là bạn đã thiết lập thành công! 🚀  
❌ **Nếu không thấy**, hãy kiểm tra lại đường dẫn trong `houdini.env` và khởi động lại Houdini.  

![image](https://github.com/user-attachments/assets/375da1c2-8cf0-467b-9558-bda407790aa0)

### **Bước 2 - Tạo thư mục lưu dữ liệu thành phố**  

Trong bước này, bạn sẽ tạo một thư mục mới để lưu dữ liệu thành phố do Houdini tạo ra. Thư mục này cũng chứa các bản sao của tệp từ **CitySample_HoudiniSource.zip**, giúp tránh ghi đè dữ liệu gốc khi tạo thêm các thành phố khác.  

#### **Thực hiện:**  
1. **Điều hướng đến thư mục chứa dữ liệu nguồn:**  
   ```
   D:\CitySampleSource
   ```
2. **Tạo một thư mục mới để lưu dữ liệu thành phố**  
   - Đặt tên thư mục là **MyCity**.  
   - Đường dẫn sẽ như sau:  
     ```
     D:\CitySampleSource\MyCity
     ```
![image](https://github.com/user-attachments/assets/b91602c3-d9d4-4b10-aaa7-49418dc619a0)
### **Sao chép dữ liệu Houdini vào thư mục MyCity**  

1. **Sao chép nội dung từ thư mục nguồn:**  
   - Điều hướng đến:  
     ```
     D:\CitySampleSource\Small_City\houdini
     ```
   - Sao chép toàn bộ nội dung trong thư mục này.  

2. **Dán vào thư mục thành phố của bạn:**  
   - Mở thư mục:  
     ```
     D:\CitySampleSource\MyCity
     ```
   - Dán các tệp đã sao chép vào đây.  

📌 **Lưu ý:** Việc sao chép này giúp bạn có một bộ dữ liệu độc lập để tạo thành phố mới mà không làm ảnh hưởng đến dữ liệu gốc của City Sample.  

---

## **Bước 3 - Bắt đầu tạo thành phố bằng cách xác định hình dạng**  

Trong Houdini, bạn sẽ sử dụng **City Layout Operator** để xác định hình dạng thành phố. Công cụ này giúp:  
✅ Định nghĩa ranh giới thành phố.  
✅ Thiết lập **đường chính (arterial splines)**.  
✅ Xác định **khu vực** và **chiều cao** của các tòa nhà.  

### **Tạo hình dạng thành phố bằng Geometry Object và Curve**  

1. **Mở Houdini** và vào **Network Pane**.  
2. **Chuột phải**, chọn **Geometry** để tạo một đối tượng hình học mới.  
3. **Dùng Curve SOP** để vẽ ranh giới thành phố.  

![image](https://github.com/user-attachments/assets/b1029b7f-0f94-4344-ad87-fb73cc7afd21)
### **Mở Geometry Object và thêm Curve Node**  

1. **Mở Houdini** và vào **Network Pane**.  
2. **Double-click** vào **Geometry Object** vừa tạo để mở **Graph Editor**.  
3. **Chuột phải trong Graph**, chọn **Tab > Curve** để thêm một **Curve Node**.  

![image](https://github.com/user-attachments/assets/c9d9fcfd-6cba-421a-b310-d960ff6372c2)
### **Vẽ hình dạng thành phố bằng Curve Node**  

1. **Chọn Curve Node** vừa tạo.  
2. **Chuyển sang Viewport**, nhấn **Left-click** để đặt các điểm tạo thành ranh giới thành phố.  
3. **Điều chỉnh kích thước phù hợp:**  
   - **Thành phố nhỏ** (~1 km rộng) → Sử dụng một khu vực nhỏ hơn.  
   - **Thành phố lớn** (~5 km rộng) → Mở rộng ranh giới với nhiều điểm hơn.  

📌 **Mẹo:**  
- Giữ **Ctrl** khi click để tạo các đoạn thẳng.  
- Nhấn **Enter** để kết thúc đường cong.  
- Sử dụng **Edit SOP** nếu cần điều chỉnh sau khi tạo.  
### **Thêm và kết nối City Layout Node**  

1. **Mở Network Pane**, chuột phải và chọn **Tab > City Layout** để thêm **City Layout Node** vào đồ thị.  
2. **Kết nối các node:**  
   - **Lấy đầu ra của Curve Node** (đã vẽ trước đó).  
   - **Kết nối vào đầu vào thứ nhất của City Layout Node**.  

✅ **Kết quả:** Houdini sẽ sử dụng các điểm từ **Curve Node** để tạo bố cục đường phố cho thành phố.  

📌 **Mẹo tối ưu:**  
- Điều chỉnh **số lượng điểm của Curve** để có layout hợp lý.  
- Kiểm tra **tham số của City Layout Node** để tinh chỉnh đường phố.  

![image](https://github.com/user-attachments/assets/0b443714-e28a-49fb-b460-dbac45e99db2)
### **Chỉnh sửa và tối ưu bố cục thành phố**  

1. **Sau khi kết nối Curve Node với City Layout Node**, Houdini sẽ tạo bố cục thành phố bên trong đường viền đã vẽ.  
2. **Chỉnh sửa hình dạng thành phố:**  
   - Chọn lại **Curve Node** trong Network Pane.  
   - Kéo các điểm trong **Viewport** để điều chỉnh ranh giới.  
   - Kết quả sẽ **tự động cập nhật** trong Viewport.  

📌 **Mẹo tối ưu:**  
- **Giảm số lượng điểm** nếu đường viền quá phức tạp, giúp tăng hiệu suất.  
- **Tạo đường cong mềm mại hơn** bằng cách sử dụng chế độ **Bezier hoặc NURBS** trong Curve Node.  
- **Xem trước giao thông** bằng cách kết hợp với **Arterial Splines** để đảm bảo đường phố hợp lý.  

### **Đặt tên cho thành phố trong City Layout Node**  

1. **Chọn City Layout Node** trong **Network Pane**.  
2. **Tìm trường văn bản** có nhãn **City Name** trong bảng thuộc tính.  
3. **Nhập tên thành phố** (ví dụ: `"MyCity"`).  

✅ **Kết quả:** Houdini sẽ sử dụng tên này để quản lý và lưu dữ liệu thành phố.  

📌 **Mẹo:**  
- Đặt tên **dễ nhớ** và **liên quan đến dự án** để quản lý nhiều thành phố khác nhau.  
- Nếu tạo **nhiều phiên bản thành phố**, bạn có thể thêm số hoặc ký hiệu như `"MyCity_V1"`, `"CyberCity_Prototype"`.  

![image](https://github.com/user-attachments/assets/e0885374-fa9e-46b5-a7cd-31dbc3e2a09e)
### **Lưu dự án Houdini**  

1. **Chọn File > Save As**.  
2. **Điều hướng đến thư mục nguồn đã tạo trước đó:**  
   ```
   D:/CitySampleSource/MyCity/
   ```
3. **Đặt tên tệp dự án**, ví dụ:  
   ```
   MyCity.hip
   ```
4. **Nhấn Save** để lưu lại tiến trình.  

✅ **Kết quả:** Dự án Houdini được lưu an toàn, giúp bạn dễ dàng tiếp tục chỉnh sửa hoặc xuất sang Unreal Engine.  

---

## **Bước 4 - Tạo hệ thống đường phố chính (City Arteries)**  

Sau khi đã xác định ranh giới thành phố, bạn cần thêm các **đường chính** (arteries) để tạo mạng lưới giao thông hợp lý.  

### **Tạo Arterial Splines**  

1. **Mở Network Pane**, **chuột phải**, chọn **Tab > Curve** để tạo **Curve Node** mới.  
2. **Chọn Curve Node**, vào **Viewport** và **nhấn Left-click** để đặt **hai điểm** vẽ tuyến đường chính.  

📌 **Mẹo tối ưu:**  
- **Vẽ nhiều đường chính** để tạo mạng lưới đa dạng.  
- **Giữ phím Shift** để điều chỉnh điểm sau khi đặt.  
- **Kết hợp với City Layout Node** để tinh chỉnh hệ thống đường phố.  

![image](https://github.com/user-attachments/assets/f21a495a-0ab9-465e-bde2-b26f2c654605)
### **Kết nối Curve Node với City Layout Node**  

1. **Chọn Curve Node** (đã vẽ tuyến đường chính trước đó).  
2. **Kéo đường kết nối từ đầu ra của Curve Node** → **đầu vào thứ hai của City Layout Node** (Arterial Splines).  

✅ **Kết quả:**  
- Tuyến đường chính sẽ được tích hợp vào bố cục thành phố.  
- Houdini sẽ tự động điều chỉnh các đường phố để phù hợp với mạng lưới giao thông.  

📌 **Mẹo tối ưu:**  
- **Giảm giao lộ không cần thiết** bằng cách tinh chỉnh đường cong của Curve Node.  
- **Điều chỉnh tham số trong City Layout Node** để thay đổi độ rộng, mật độ đường chính.  
- **Thêm nhiều Arterial Splines** để tạo các trục đường chính đa hướng.  
![image](https://github.com/user-attachments/assets/f8730921-9a21-4c3e-b4cd-573191faac42)
### **Thêm Nhiều Tuyến Đường Chính (Arterial Splines) và Kết Nối Với City Layout**  

Để tối ưu hệ thống giao thông của thành phố, bạn có thể thêm nhiều tuyến đường chính bằng cách sử dụng **Curve Node** và **Merge Node**.  

#### **Các bước thực hiện:**  

1. **Tạo thêm Curve Nodes để vẽ nhiều tuyến đường chính hơn:**  
   - Chuột phải trong **Network Pane** > **Tab > Curve**.  
   - Vẽ các tuyến đường mới trong **Viewport** bằng **Left-click**.  
   - Lặp lại bước này nếu muốn thêm nhiều tuyến đường.  

2. **Thêm Merge Node để hợp nhất các tuyến đường chính:**  
   - Chuột phải trong **Network Pane** > **Tab > Merge**.  
   - Kết nối đầu ra của **các Curve Nodes** vào **Merge Node**.  

3. **Kết nối Merge Node với City Layout Node:**  
   - Lấy đầu ra của **Merge Node** → Kết nối vào **đầu vào thứ hai (Arterial Splines) của City Layout Node**.  

✅ **Kết quả:**  
- Thành phố có nhiều tuyến đường chính hơn, giúp hệ thống giao thông hợp lý và mượt mà hơn.  
- Houdini sẽ tự động điều chỉnh các đường phố để phù hợp với mạng lưới giao thông mới.  

📌 **Mẹo tối ưu:**  
- **Tránh đặt quá nhiều tuyến đường chính**, vì có thể làm thành phố bị chia nhỏ không hợp lý.  
- **Điều chỉnh tham số của City Layout Node** để kiểm soát chiều rộng và mật độ đường.  
- **Sử dụng các đường cong thay vì đường thẳng**, giúp thành phố có vẻ tự nhiên hơn.  

![image](https://github.com/user-attachments/assets/11ba50a2-65c9-450c-8a7e-d45050fed43e)
### **Tùy chỉnh hình dạng thành phố và hệ thống đường phố chính**  

Sau khi đã tạo các tuyến đường chính (**Arterial Splines**), bạn có thể **điều chỉnh hình dạng thành phố** và **tinh chỉnh đường phố** để tối ưu bố cục tổng thể.  

#### **1. Chỉnh sửa hình dạng thành phố:**  
- **Chọn Curve Node** đã dùng để xác định ranh giới thành phố.  
- **Chỉnh sửa điểm (control points)** của đường cong bằng cách **click và kéo** trong Viewport.  
- **Điều chỉnh kích thước tổng thể**, đảm bảo đường phố không bị cắt xén bất hợp lý.  

#### **2. Tinh chỉnh hệ thống đường chính:**  
- **Chọn các Curve Nodes** đã tạo để xác định các tuyến đường chính.  
- **Di chuyển, thêm hoặc xóa điểm** để thay đổi hướng đi của các tuyến đường.  
- **Thử nghiệm với nhiều cách bố trí đường phố** để tạo giao thông hợp lý.  

#### **3. Tùy chỉnh thêm bằng City Layout Properties:**  
- **Điều chỉnh tham số trong City Layout Node** để kiểm soát:  
  - **Độ rộng đường chính & phụ.**  
  - **Mật độ và kiểu bố trí đường phố.**  
  - **Cấu trúc của các khu vực (zones) trong thành phố.**  

✅ **Kết quả:**  
- Thành phố có hình dạng tự nhiên hơn.  
- Đường phố được tối ưu, tránh giao lộ phức tạp hoặc bất hợp lý.  
- Hệ thống giao thông cân đối giữa các khu vực trung tâm và vùng ven.  

📌 **Mẹo tối ưu:**  
- **Tạo đường cong mềm mại cho Arterial Splines** để tránh bố cục thành phố bị gò bó.  
- **Thử nghiệm với các tham số đường phố trong City Layout** để tìm được cấu trúc phù hợp.  
- **Xem trước bằng viewport trong Houdini** để đánh giá tổng quan bố cục trước khi tiếp tục.  

![image](https://github.com/user-attachments/assets/3c95ecfd-7e7f-4940-8504-39bb25cab749)
### **Tối ưu hệ thống đường phố bằng Road Network Options**  

Sau khi đã thiết lập đường phố cơ bản, bước này giúp bạn **điều chỉnh mật độ và hướng đường**, đồng thời **tinh chỉnh giao lộ** để đảm bảo lưu thông mượt mà.  

---

### **1. Điều chỉnh mật độ và góc đường phố**  
- **Chọn City Layout Node** trong Network Pane.  
- **Tùy chỉnh mật độ (Density)** để thay đổi lưới chia nhỏ thành phố:  
  - **Mật độ cao** → Nhiều đường nhỏ hơn, phù hợp với khu trung tâm.  
  - **Mật độ thấp** → Ít đường hơn, phù hợp với khu dân cư hoặc ngoại ô.  
- **Chỉnh góc đường phố (Angle Property)** để tạo mạng lưới đường tự nhiên hơn:  
  - **Góc thẳng (90°)** → Phù hợp với thành phố lưới ô vuông như New York.  
  - **Góc nghiêng (30° - 60°)** → Tạo cảm giác tự nhiên hơn như các khu đô thị hiện đại.  

---

### **2. Kiểm tra và sửa lỗi hệ thống giao thông**  
- **Xem trước bố cục đường phố** trong viewport để phát hiện lỗi.  
- **Kiểm tra các điểm giao nhau** của nhiều đường chính:  
  - **Loại bỏ hoặc điều chỉnh các giao lộ quá phức tạp.**  
  - **Đảm bảo không có đường cụt hoặc xung đột với bố cục thành phố.**  
- **Sử dụng Full Preview Mode** để đánh giá hệ thống giao thông tổng thể.  

---

### **3. Sử dụng Road Network Options để tinh chỉnh giao lộ**  
- **Hợp nhất các khu vực nhỏ (Merge City Blocks):**  
  - Giúp tạo lô đất rộng hơn, tránh quá nhiều ngõ hẻm nhỏ.  
- **Hợp nhất các đường gần giao lộ (Merge Roads Near Intersections):**  
  - Làm mượt các điểm giao nhau, giúp phương tiện di chuyển thuận lợi hơn.  

✅ **Kết quả:**  
- Mạng lưới đường phố rõ ràng, logic và không bị lỗi.  
- Giao thông hợp lý với mật độ và góc đường phù hợp.  
- Thành phố có bố cục tự nhiên, hỗ trợ tốt cho các bước tiếp theo.  


![image](https://github.com/user-attachments/assets/3412f3a3-9bf0-40d6-b88e-43b6df0d245c)
### **Bật Chế Độ Full Preview để Kiểm Tra Đường Phố**  

✅ **Mục đích:**  
Chế độ **Full Preview** giúp hiển thị toàn bộ hệ thống đường phố sau khi đã được xử lý và tối ưu. Điều này giúp bạn kiểm tra lỗi giao lộ, mật độ đường và bố cục tổng thể trước khi tiến xa hơn.  

---

### **Hướng Dẫn Bật Full Preview**  
1. **Chọn City Layout Node** trong Network Pane.  
2. **Mở City Layout Properties** ở phía trên Network Pane.  
3. **Đi đến mục `preview_options`**.  
4. **Tích vào ô "Full Preview"** để bật chế độ xem chi tiết.  

---

### **Lưu Ý Khi Sử Dụng Full Preview**  
- 🔹 **Ưu điểm:**  
  - Giúp bạn thấy toàn bộ kết quả cuối cùng sau khi Houdini xử lý.  
  - Dễ phát hiện lỗi trong hệ thống đường phố và bố cục thành phố.  
- 🔹 **Nhược điểm:**  
  - **Giảm hiệu suất làm việc** vì Houdini phải tính toán nhiều hơn.  
  - **Tương tác viewport chậm hơn**, đặc biệt với thành phố lớn.  

---

### **Mẹo Tối Ưu Khi Dùng Full Preview**  
✅ **Chỉ bật khi cần kiểm tra tổng thể**, tắt khi chỉnh sửa để tránh giật lag.  
✅ **Sử dụng bộ lọc xem trước** để hiển thị từng phần của thành phố thay vì toàn bộ.  
✅ **Tối ưu hệ thống đường trước** (đặc biệt là Merge Blocks và Merge Roads) để giảm tải khi bật Full Preview.  

---

![image](https://github.com/user-attachments/assets/225dff7d-c0d6-4e32-8fba-44817afb5ebe)
![image](https://github.com/user-attachments/assets/c880160b-5dd5-4436-8499-7863f2cc2dbf)
### **Tùy Chỉnh Hệ Thống Đường Phố bằng Road Network Options**  

✅ **Mục tiêu:**  
Điều chỉnh **Road Network Options** để tối ưu hệ thống giao thông, tránh lỗi **giao lộ chồng lấn**, **đường quá ngắn**, hoặc **đường quá gần nhau**.  

---

### **1️⃣ Mở Road Network Options**  
1. **Chọn City Layout Node** trong Network Pane.  
2. **Chuyển sang tab "Road Network Options"** trong City Layout Properties.  
3. **Chỉnh sửa các thuộc tính quan trọng:**  

---

### **2️⃣ Các Cài Đặt Quan Trọng**  

🔹 **Merge Blocks (Hợp nhất các ô phố)**  
- ✅ Hợp nhất các khu phố nhỏ để tránh có quá nhiều con hẻm hẹp.  
- ✅ Giảm số lượng đường không cần thiết, giúp quy hoạch thành phố hợp lý hơn.  

🔹 **Merge Roads Near Intersections (Làm mượt giao lộ)**  
- ✅ Kết hợp những đường gần nhau để tránh tình trạng quá nhiều đường hội tụ vào một điểm.  
- ✅ Tạo các góc giao lộ hợp lý, giúp giao thông mượt mà.  

🔹 **Minimum Road Length (Độ dài tối thiểu của đường phố)**  
- ✅ Loại bỏ những con đường quá ngắn, không cần thiết.  
- ✅ Giúp bố cục thành phố gọn gàng, giảm tình trạng các đường cụt nhỏ.  

🔹 **Minimum Intersection Angle (Góc giao lộ tối thiểu)**  
- ✅ Tránh tạo các giao lộ với góc quá hẹp (<30°), dễ gây tắc nghẽn.  
- ✅ Giữ góc giao lộ hợp lý để xe cộ di chuyển dễ dàng hơn.  

---

### **3️⃣ Kiểm Tra & Hiệu Chỉnh**  
✅ **Sử dụng chế độ Full Preview** để kiểm tra giao lộ và bố cục đường phố.  
✅ **Điều chỉnh thủ công** nếu thấy khu vực nào có đường phố hoặc giao lộ chưa hợp lý.  
✅ **Kết hợp với hệ thống AI giao thông** để đảm bảo đường phố tối ưu cho phương tiện và người đi bộ.  

-

![image](https://github.com/user-attachments/assets/6b5b4c51-8c8b-4dc1-a8ab-a64d3f9b4a30)
### **Tối Ưu Hóa Đường Phố với Arterial Splines & Road Network Properties**  

✅ **Mục tiêu:**  
- **Chia thành phố thành các khu vực hợp lý** bằng cách sử dụng nhiều **arterial splines** (đường trục chính).  
- **Tối ưu hệ thống giao thông** bằng cách **hợp nhất đường phố** và **giảm giao lộ phức tạp**.  

---

### **1️⃣ Sử Dụng Nhiều Arterial Splines**  
🔹 Trong ví dụ, thành phố được chia thành **bốn khu vực** với các đường trục chính.  
🔹 Mỗi khu vực có các đường đi theo **hướng khác nhau**, giúp lưu thông dễ dàng hơn.  
🔹 Tuy nhiên, **việc có nhiều đường giao nhau** có thể gây ra **tắc nghẽn tại giao lộ**.  

---

### **2️⃣ Tối Ưu Giao Lộ & Kết Nối Đường Phố**  

1️⃣ **Hợp nhất city blocks để tránh quá nhiều đường nhỏ:**  
   - **Tăng giá trị "Merge Blocks"** để gộp các khu phố nhỏ thành khu lớn hơn.  
   - **Giảm số lượng giao lộ không cần thiết**, giúp lưu thông tốt hơn.  

2️⃣ **Làm mượt giao lộ bằng cách Merge Roads Near Intersections:**  
   - Khi hai hoặc nhiều đường hội tụ, sử dụng **Merge Roads** để giảm số lượng giao lộ phức tạp.  
   - Điều chỉnh góc giao lộ để tránh tạo đường quá hẹp (<30°).  

3️⃣ **Điều chỉnh số lượng & hướng arterial splines:**  
   - Tránh đặt quá nhiều **arterial splines** nếu không cần thiết.  
   - **Tối ưu hóa hướng đường phố** để tạo dòng chảy giao thông hợp lý.  

---

### **3️⃣ Kiểm Tra & Hiệu Chỉnh**  
✅ **Dùng chế độ Full Preview** để kiểm tra kết quả và sửa lỗi nếu có.  
✅ **Quan sát kỹ các khu vực giao lộ lớn** và xem có cần điều chỉnh không.  
✅ **Kết hợp hệ thống AI giao thông** để tự động tối ưu hóa đường phố và tránh ùn tắc.  

---

![image](https://github.com/user-attachments/assets/0f5d41d8-8c4f-4c34-b63c-416c6c9b780d)
### **Bước 6 - Vẽ Vùng Thành Phố & Điều Chỉnh Cityscape**  

✅ **Mục tiêu:**  
- **Định nghĩa các khu vực chức năng** trong thành phố bằng cách vẽ **City Zones**.  
- **Thiết lập chiều cao & hình dạng công trình** bằng **City Zone Operator**.  

---

### **1️⃣ Tạo Khu Vực Thành Phố (City Zone)**  

🔹 Trong **Network Pane**, tạo một **Curve Node** để vẽ khu vực muốn phân vùng.  
🔹 **Dùng Viewport** để vẽ một vùng bao quanh khu vực cần định nghĩa.  
🔹 Kết nối **Curve Node** với **City Zone Operator**.  

---

### **2️⃣ Thiết Lập Thuộc Tính City Zone**  

🔸 **Chiều cao công trình:**  
   - Dùng **City Zone Properties** để thiết lập chiều cao tòa nhà.  
   - Sử dụng **nhiều điểm trên đồ thị** để kiểm soát độ cao thay đổi theo vị trí.  

🔸 **Kiểu tòa nhà:**  
   - Xác định các loại công trình khác nhau trong từng khu vực.  
   - Ví dụ: khu dân cư, thương mại, cao ốc văn phòng, khu công nghiệp...  

---

### **3️⃣ Điều Chỉnh Tổng Thể Cityscape**  

✅ **Sử dụng Viewport để tinh chỉnh vùng thành phố.**  
✅ **Điều chỉnh mật độ & chiều cao công trình** để có bố cục hợp lý.  
✅ **Tích hợp AI để tự động tối ưu hóa việc phân vùng thành phố.**  

---

### **Bước 6.1 - Thêm City Zone Operator**  

✅ **Mục tiêu:**  
- **Tạo vùng thành phố** bằng cách sử dụng **City_Zone Operator**.  
- **Kết nối vùng này** với **City Layout** để xác định khu chức năng.  

---

### **1️⃣ Thêm City Zone Operator**  

🔹 Trong **Network Pane**, **chuột phải** → **Thêm City_Zone Operator**.  
🔹 **Kết nối các node:**  
   1. **Curve Node** → **City_Zone Node**.  
   2. **City_Zone Node** → **City Layout Node** (cổng *City Zones* - Input 3).  

---

### **2️⃣ Điều Chỉnh Thuộc Tính City Zone**  

🔸 **Chỉnh sửa Viewport** để mở rộng hoặc thu nhỏ khu vực.  
🔸 **Thiết lập chiều cao & loại công trình** bằng thuộc tính của **City_Zone Operator**.  
🔸 **Kết hợp với AI để tự động hóa quá trình phân vùng & tối ưu chiều cao công trình**.  


![image](https://github.com/user-attachments/assets/bfd42e3e-421c-4be3-944c-0540673fcd3e)
### **Bước 6.2 - Điều Chỉnh Thuộc Tính City Zone**  

✅ **Mục tiêu:**  
- Chỉnh sửa **thuộc tính của City Zone** để kiểm soát chiều cao & loại công trình.  

---

### **1️⃣ Chỉnh Sửa City Zone Node**  

🔹 Trong **Network Pane**, chọn **City Zone Node**.  
🔹 **Thuộc tính của City Zone** sẽ hiển thị ở **pane phía trên Network Graph**.  

---

### **2️⃣ Tùy Chỉnh City Zone**  

🔸 **Điều chỉnh chiều cao tòa nhà:**  
   - Dùng **graph chỉnh độ cao** để thay đổi profile skyline của thành phố.  
   - Có thể tạo hiệu ứng **cao tầng ở trung tâm, thấp dần ra ngoại ô**.  

🔸 **Thay đổi kiểu kiến trúc:**  
   - Xác định từng loại công trình như **dân cư, thương mại, công nghiệp**.  
   - Dùng **AI hoặc procedural rules** để tự động sinh loại tòa nhà phù hợp.  

---
![image](https://github.com/user-attachments/assets/dbd07614-2ea7-467d-83dd-12a9297fab5e)

### **Bước 6.3 - Điều Chỉnh Chiều Cao & Hình Dạng Khu Vực**  

✅ **Mục tiêu:**  
- **Tùy chỉnh chiều cao tối đa** cho từng khu vực.  
- **Điều chỉnh dạng đường cong chiều cao** để tạo hiệu ứng tự nhiên.  

---

### **1️⃣ Các Thuộc Tính Chính của City Zone**  

🔹 **Height** → Xác định **chiều cao tối đa** của vùng.  
🔹 **Point No.** → Chọn điểm trên **biểu đồ chiều cao** (mặc định có 2 điểm: 0 và 1).  
🔹 **Thêm điểm mới** → Click vào biểu đồ để tự động thêm điểm kiểm soát.  
🔹 **Position & Value** → Di chuyển điểm dọc **trục X (vị trí)** và **trục Y (chiều cao)**.  
🔹 **Interpolation** → Chọn kiểu nội suy giúp **tạo độ mượt cho hình dạng chiều cao**.  

---

### **2️⃣ Cách Tạo Hiệu Ứng Chiều Cao Thành Phố**  

🔸 **Hiệu ứng đô thị cổ điển:**  
   - Cao ở trung tâm, thấp dần ra ngoại ô.  
   - Sử dụng **interpolation tuyến tính hoặc ease-in/out** để tạo chuyển đổi mượt mà.  

🔸 **Hiệu ứng Skyline hiện đại:**  
   - Pha trộn **cao ốc, tòa nhà vừa và thấp** bằng cách điều chỉnh nhiều điểm trên graph.  
   - Sử dụng **random noise hoặc AI procedural** để sinh chiều cao tự nhiên.  

---
![image](https://github.com/user-attachments/assets/4b22b960-00ad-4f61-b057-34b669c1b0ac)
### **Bước 6.4 - Tạo Nhiều Khu Vực Khác Nhau** (Tùy chọn)  

✅ **Mục tiêu:**  
- **Thêm nhiều vùng** với chiều cao và loại công trình khác nhau.  
- **Kết hợp nhiều City Zone** vào City Layout bằng **Merge node**.  

---

### **1️⃣ Thêm Các City Zone Mới**  
🔹 **Lặp lại các bước trước** để tạo **Curve** và **City Zone operator**.  
🔹 **Vẽ thêm vùng mới** để phân chia khu vực **dân cư, thương mại, công nghiệp**.  

---

### **2️⃣ Hợp Nhất Các Khu Vực**  
🔸 Dùng **Merge Node** để gom nhiều **City Zone Node** lại.  
🔸 Kết nối **Merge Node** vào **Input 3 (City Zones) của City Layout**.  
🔸 Kiểm tra trong Viewport để xem các khu vực có hợp lý không.  

---

### **🔥 Mẹo Tối Ưu**  
✅ **Tạo phân vùng đô thị tự nhiên:** Dùng **Noise hoặc AI** để sinh chiều cao theo quy tắc thực tế.  
✅ **Tối ưu Merge Node:** Gộp nhiều Zone nhưng vẫn giữ tính linh hoạt trong chỉnh sửa.  

![image](https://github.com/user-attachments/assets/57d56942-1733-4ebf-9ca3-95aeae7411fe)
### **Bước 7 - Vẽ Tuyến Đường Cao Tốc Qua Thành Phố**  

✅ **Mục tiêu:**  
- **Thêm đường cao tốc** để cải thiện giao thông.  
- **Kết nối lối vào và lối ra** với các tuyến đường chính.  
- **Sử dụng Curve và Freeway Util Curve Attribute operator**.  

---

### **1️⃣ Tạo Đường Cao Tốc**  
🔹 **Thêm Curve Node** trong **Network Pane**.  
🔹 **Vẽ tuyến đường cao tốc** bằng cách nhấp các điểm trong Viewport.  
🔹 Điều chỉnh hình dạng đường để phù hợp với thành phố.  

---

### **2️⃣ Thêm Các Lối Vào Và Lối Ra**  
🔸 Sử dụng **Freeway Util Curve Attribute operator**.  
🔸 **Kết nối Curve vào Freeway Util** để xác định thuộc tính đường cao tốc.  
🔸 **Gắn Freeway vào City Layout** để tích hợp vào hệ thống đường phố.  

---

### **🔥 Mẹo Tối Ưu**  
✅ **Giữ khoảng cách hợp lý** giữa đường cao tốc và khu vực trung tâm.  
✅ **Tạo các đoạn cong hợp lý** để xe di chuyển mượt mà.  
✅ **Sử dụng AI hoặc thuật toán tối ưu** để tự động sinh tuyến đường tối ưu.  
![image](https://github.com/user-attachments/assets/155b1e1d-e2f6-4844-bce5-7e282d97ff99)
### **3️⃣ Cải Thiện Hình Ảnh Tuyến Đường Cao Tốc**  
✅ **Sử dụng Polywire và Merge nodes** để hiển thị tuyến đường rõ ràng hơn.  
✅ **Điều chỉnh Wire Radius** để tăng kích thước đường cao tốc trong Viewport.  
✅ **Hợp nhất tuyến đường** với layout thành phố bằng Merge node.  

---

🔹 **Lợi ích của việc hiển thị tuyến đường rõ ràng:**  
- Giúp kiểm tra **kết nối giữa cao tốc và đường thành phố**.  
- Tránh các lỗi về **giao điểm hoặc chồng lấn không mong muốn**.  
- Dễ dàng **chỉnh sửa và tinh chỉnh** trước khi xuất sang Unreal Engine.  
![image](https://github.com/user-attachments/assets/aefcec06-ce28-4f3e-ba75-e48fc3c7be0e)

### **4️⃣ Thêm Thuộc Tính Đường Cao Tốc**  
✅ **Sử dụng menu chuột phải** để thêm **Freeway Util Curve Attribute** vào biểu đồ.  
✅ **Kết nối Curve node** với **Freeway Util Curve Attribute** để xác định tuyến đường cao tốc.  
✅ **Tinh chỉnh thuộc tính** để kiểm soát **độ cong, làn đường, và điểm kết nối với thành phố**.  

---

🔹 **Tại sao cần Freeway Util Curve Attribute?**  
- Xác định **hành vi và quy tắc** của đường cao tốc.  
- Giúp **kết nối hợp lý** với mạng lưới đường trong thành phố.  
- Cho phép **tùy chỉnh chi tiết**, như số làn đường, độ cong, và tốc độ di chuyển.  
![image](https://github.com/user-attachments/assets/c4d6feed-75d8-418d-8596-00f198a14377)
### **5️⃣ Điều Chỉnh Thuộc Tính Đường Cao Tốc**  

Khi chọn **Freeway Util Curve Attribute**, có hai thuộc tính chính cần điều chỉnh:  

✅ **Lane Count** – Xác định số làn xe trên đường cao tốc.  
✅ **Ramp Type** – Kiểm soát kiểu kết nối giữa đường cao tốc và các tuyến đường chính.  

---

🔹 **Tại sao điều chỉnh các thuộc tính này quan trọng?**  
- **Lane Count** giúp **quy hoạch mật độ giao thông**, tránh ùn tắc trong thành phố.  
- **Ramp Type** quyết định cách **xe nhập và thoát khỏi cao tốc**, ảnh hưởng đến luồng di chuyển.  

![image](https://github.com/user-attachments/assets/41c8a525-23aa-4b40-8eb1-328b47767d96)
### **6️⃣ Hoàn Thiện Định Tuyến Cao Tốc**  

🔹 **Cấu hình quan trọng:**  
- **Number of Lanes:** Chọn **4 hoặc 6 làn** tùy vào mật độ giao thông mong muốn.  
- **Closed:** Nếu muốn **đường cao tốc là một vòng khép kín**, bật tùy chọn này.  

📌 **Lưu ý khi không đóng vòng cao tốc:**  
- Đảm bảo hai đầu **kết nối với đường chính (arterial roads, màu đỏ)**.  
- Cao tốc phải **khớp với hướng lưu thông tổng thể** của hệ thống đường.  

✅ **Bước hoàn tất:**  
- **Xóa** các node **Merge và Polywire** (chỉ dùng để quan sát).  
- **Kết nối** Curve node với Freeway Util Curve Attributes node để **hoàn thành cấu trúc đường cao tốc**.  

![image](https://github.com/user-attachments/assets/9fd3e9d6-8ce0-41f3-aed8-3116b67eaee2)
### **8️⃣ Kết Hợp Dữ Liệu Trong City Processor**  

🚀 **Bước quan trọng nhất!** Đây là nơi **tổng hợp tất cả dữ liệu đã thiết lập** về:  
✅ **Hình dạng thành phố**  
✅ **Hệ thống đường chính & cao tốc**  
✅ **Khu vực quy hoạch (zones) & chiều cao tòa nhà**  

🔹 **Sử dụng City Processor Operator**  
1. **Mở Network pane** → **Chuột phải** → **Thêm node City Processor**.  
2. **Kết nối đầu vào:**  
   - **City Layout** (định dạng đường phố)  
   - **Freeway Util Curve Attributes** (hệ thống cao tốc)  
   - **City Zone** (khu quy hoạch)  

📌 **Lưu ý:**  
- Kiểm tra lỗi hiển thị & điều chỉnh nếu cần.  
- Có thể **tinh chỉnh lại vị trí đường** để tối ưu kết nối.
  ### **Bước 8 - Tập hợp các đầu vào trong City Processor**  

Bây giờ bạn đã hoàn thành nền móng cho thành phố của mình—bao gồm **hình dạng, mạng lưới đường, hệ thống cao tốc và phân vùng**—đã đến lúc tổng hợp tất cả bằng cách sử dụng **City Processor**.  

#### **🛠 Các bước thiết lập City Processor**  
1️⃣ **Thêm node City Processor**  
   - Trong **Network pane**, nhấp chuột phải → **Thêm "City Processor" node**.  

2️⃣ **Kết nối các đầu vào cần thiết**  
   - **City Layout** → Đầu vào thứ nhất của City Processor  
   - **Freeway Util Curve Attributes** → Đầu vào thứ hai  
   - **City Zones** (kết nối Merge node nếu có nhiều vùng) → Đầu vào thứ ba  

3️⃣ **Cấu hình City Processor**  
   - Chọn **node City Processor**.  
   - Mở **Parameters Pane** (phía trên network).  
   - Điều chỉnh các thông số như **chiều rộng đường, mật độ ô lưới, kích thước khối nhà**.  

4️⃣ **Bật chế độ xem toàn diện (Full Preview Mode)**  
   - Trong **Preview Options**, bật **Full Preview** để hiển thị chính xác hơn.  

💡 **Mẹo:** Nếu các ngã tư đường trông quá chật chội hoặc không thẳng hàng, hãy chỉnh lại **Road Network Options** hoặc **Arterial Splines** để tối ưu bố cục.  


![image](https://github.com/user-attachments/assets/f048d129-180f-4972-8abb-b3fd90354466)
### **🔧 Chuyển Houdini sang chế độ "Manual" để kiểm soát quá trình cook**  

Mặc định, Houdini tự động cập nhật (cook) nội dung sau mỗi thao tác. Tuy nhiên, khi làm việc với **City Processor**, bạn nên **chuyển sang chế độ "Manual"** để tránh việc Houdini cook dữ liệu chưa hoàn chỉnh, gây chậm hoặc lỗi.  

#### **📌 Cách chuyển Houdini sang chế độ Manual:**  
1️⃣ **Tìm hộp chọn chế độ cook** ở **góc dưới bên phải** cửa sổ Houdini.  
2️⃣ Nhấp vào **Auto Update** (hoặc biểu tượng dấu chấm than).  
3️⃣ Chọn **Manual** để dừng quá trình cook tự động.  

🛠 **Lợi ích của Manual Mode:**  
✅ Tránh Houdini cook mỗi khi bạn thêm hoặc chỉnh sửa node.  
✅ Giảm tải CPU, giúp làm việc với các thành phố lớn mượt hơn.  
✅ Chỉ cook khi bạn đã hoàn thành kết nối tất cả đầu vào cần thiết.  

📌 **Lưu ý:** Sau khi hoàn tất thiết lập City Processor, hãy nhấn **"Cook" hoặc "Update"** để cập nhật toàn bộ thành phố trong Houdini. 🚀
![image](https://github.com/user-attachments/assets/1b0b5a9f-2dd8-468c-8285-39a842698cf5)
### **🔗 Kết nối City Layout với City Processor trong Houdini**  

Bước này sẽ tổng hợp tất cả các dữ liệu của thành phố bằng cách sử dụng **City Processor**.  

#### **📌 Các bước thực hiện:**  
1️⃣ **Mở Network Pane** trong Houdini.  
2️⃣ **Nhấp chuột phải** vào vùng trống, chọn **"Add Node" → "City Processor"** để thêm node xử lý thành phố.  
3️⃣ **Kết nối đầu ra thứ hai của City Layout** *(output 2 - City Blocks & Roads)* **vào đầu vào thứ nhất của City Processor**.  
   - **City Layout (Output 2) → City Processor (Input 1)**  

📌 **Lưu ý:**  
- **City Layout Output 2** chứa dữ liệu về hệ thống đường phố, block nhà, zone, freeway...  
- **City Processor** sẽ xử lý và tối ưu hóa thành phố dựa trên dữ liệu đầu vào này.  

![image](https://github.com/user-attachments/assets/255b0614-3d8f-479a-95e7-61f7a31628f8)
### **🔗 Kết nối Freeway Util Curve Attributes với City Processor**  

Ở bước này, chúng ta sẽ tiếp tục đưa dữ liệu **Freeway** vào **City Processor** để hoàn chỉnh hệ thống đường cao tốc trong thành phố.  

#### **📌 Các bước thực hiện:**  
1️⃣ Trong **Network Pane**, xác định **Freeway Util Curve Attributes Node**.  
2️⃣ **Kéo dây kết nối đầu ra** của **Freeway Util Curve Attributes** *(Output 1)* vào **đầu vào thứ hai của City Processor** *(Input 2 - Freeway Data)*.  

📌 **Lưu ý:**  
- **Input 2 của City Processor** dùng để nhận dữ liệu **đường cao tốc**.  
- Đảm bảo **đường cao tốc có kết nối hợp lý với hệ thống đường chính** trong City Layout.  

🚀 **Sau khi hoàn thành kết nối, hệ thống freeway sẽ được tích hợp vào thành phố!**
![image](https://github.com/user-attachments/assets/2a85a636-fa49-495c-b343-13a9a11877af)
### **🔄 Chuyển Houdini về chế độ Auto Update**  

Sau khi đã kết nối tất cả các đầu vào cần thiết vào **City Processor**, bây giờ ta sẽ chuyển Houdini trở lại chế độ **Auto Update** để tiến hành xử lý dữ liệu và hiển thị kết quả.  

#### **📌 Các bước thực hiện:**  
1️⃣ **Tìm thanh trạng thái ở góc dưới bên phải** của cửa sổ Houdini.  
2️⃣ Nhấn vào **hộp chọn chế độ cập nhật** *(Update Mode)*.  
3️⃣ Chọn **Auto Update**.  

📌 **Lưu ý:**  
- Khi chuyển sang **Auto Update**, Houdini sẽ **tự động cook dữ liệu** và cập nhật giao diện với các thay đổi mới nhất.  
- Nếu thành phố có quy mô lớn, việc này có thể mất một chút thời gian tùy vào cấu hình máy.  

🚀 **Sau khi hoàn tất, bạn sẽ thấy thành phố của mình hiển thị với tất cả đường phố, xa lộ và các khu vực đã được định nghĩa!**
![image](https://github.com/user-attachments/assets/857b7c0f-3a80-4e29-a715-b3a77da6164a)

### **👀 Xem trước thành phố đã tạo**  

Sau khi **City Processor** hoàn tất quá trình xử lý, bạn có thể xem trước thành phố đã được tạo dựa trên tất cả dữ liệu đầu vào từ các bước trước đó.  

#### **🔍 Những điểm quan trọng cần kiểm tra trong bản xem trước:**  
✅ **Đường cao tốc (Freeway)**: Được đặt đúng vị trí và có kết nối hợp lý với các tuyến đường chính.  
✅ **Đường chính (Arterial Roadways)**: Hai tuyến đường lớn kéo dài xuyên suốt thành phố.  
✅ **Bố cục đường phố**: Các khu vực khác nhau có hướng đường phố khác nhau, tạo sự đa dạng.  
✅ **Khu vực thành phố (City Zones)**:  
- Một khu vực có **các tòa nhà cao tầng** tập trung.  
- Một khu vực có **sự tăng dần về chiều cao**, nhưng không quá cao như khu vực đầu tiên.  

📌 **Lưu ý:**  
- Nếu có bất kỳ lỗi nào trong việc hiển thị đường phố hoặc bố cục, bạn có thể quay lại và chỉnh sửa các node trong **City Layout** hoặc **Freeway Util Curve Attributes** để tinh chỉnh kết quả.  
- Nếu cần điều chỉnh tỷ lệ hoặc hướng phát triển của thành phố, hãy kiểm tra lại các thông số **City Processor** để đảm bảo mọi thứ hiển thị đúng như mong đợi.  

🚀 **Sau khi xác nhận mọi thứ đã ổn, bạn có thể tiếp tục đến bước tiếp theo: Thêm các tòa nhà vào thành phố!**
![image](https://github.com/user-attachments/assets/62cea257-606b-423d-a15b-d60f08827add)


### **🚦 Bước 9 - Kết nối Đường Cao Tốc (Freeway) với Thành Phố**  

Sau khi **City Processor** đã xử lý thành phố dựa trên các dữ liệu từ các node trước đó, bạn cần đảm bảo rằng **đường cao tốc (Freeway)** được kết nối hợp lý với các tuyến đường trong thành phố.  

#### **🛠 Các bước thực hiện:**  

1️⃣ **Mở Network Graph của City Processor:**  
   - Trong **Network pane**, double-click vào **City Processor node** để mở **network graph**.  
   - Tìm đến phần **Freeway** trong graph để thực hiện các chỉnh sửa cần thiết.  

2️⃣ **Tạo kết nối giữa Freeway và đường phố:**  
   - Nếu đường cao tốc chưa kết nối với mạng lưới đường phố, bạn cần thêm các đường **ramp** (lối ra vào).  
   - Sử dụng **Curve node** để vẽ các đoạn đường nối từ Freeway vào các tuyến đường chính.  
   - Kết hợp với **Merge node** để gom các đường ramp lại và nối với **City Layout node**.  

3️⃣ **Kiểm tra kết nối trong Viewport:**  
   - Chuyển sang chế độ **Full Preview** để kiểm tra xem các kết nối có hợp lý không.  
   - Đảm bảo các lối ra/vào không bị cắt đứt hoặc quá dốc, gây ảnh hưởng đến lưu thông trong thành phố.  

📌 **Mẹo tối ưu:**  
✅ Nếu đường cao tốc là một vòng khép kín, hãy đảm bảo có ít nhất **2-3 điểm kết nối** với thành phố để tránh tắc nghẽn giao thông.  
✅ Nếu Freeway có làn xe riêng (4-6 lanes), hãy kiểm tra rằng chiều rộng phù hợp và không xâm phạm khu vực khác của thành phố.  
✅ Dùng **Road Network Options** trong City Layout để tối ưu hóa kết nối đường bộ.  

🚀 **Sau khi hoàn tất, bạn có thể tiếp tục bước tiếp theo: Tinh chỉnh chi tiết và tạo các mô hình tòa nhà!**
![image](https://github.com/user-attachments/assets/92fd07e2-abe4-4189-b732-7a2fc139ecd7)
### **🔧 Chỉnh sửa Freeway trong City Processor**  

1️⃣ **Tìm phần FREEWAY OUTPUT**  
   - Trong **Network Graph của City Processor**, cuộn xuống vùng có comment **(blue section) FREEWAY OUTPUT**.  
   - Tìm **FREEWAY node** trong khu vực này.  

2️⃣ **Cho phép chỉnh sửa nội dung của node**  
   - Nhấp chuột phải vào **FREEWAY node**.  
   - Chọn **Allow Editing of Contents** từ menu ngữ cảnh.  
   - Điều này giúp bạn có thể thay đổi cách thức kết nối của đường cao tốc với thành phố.  

✅ **Bước tiếp theo:** Tiến hành chỉnh sửa và kết nối Freeway với đường phố bằng cách thêm **Ramp Connections!** 🚗💨
![image](https://github.com/user-attachments/assets/10c63fb9-9e4f-4f54-8949-c1ca094289df)
### **🛣️ Mở FREEWAY Node để Kết Nối Cao Tốc**  

1️⃣ **Mở Network của FREEWAY Node**  
   - **Double-click** vào **FREEWAY node** để mở biểu đồ bên trong.  
   - Nhìn về phía **trái**, dưới vùng **blue notes** có tên:  
     - **Process Freeway**  
     - **Connections**  
     - **Ramp**  

2️⃣ **Tìm connections_blank node**  
   - Trong khu vực này, tìm **connections_blank node**.  
   - Node này dùng để xác định các điểm kết nối giữa cao tốc và đường thành phố.  

✅ **Bước tiếp theo:** Chỉnh sửa **connections_blank** để tạo điểm nối hợp lý cho Freeway vào thành phố! 🚧
![image](https://github.com/user-attachments/assets/fc47b5e8-1328-41a0-8400-586e10721040)
### **🔧 Chỉnh Sửa Kết Nối Cao Tốc**  

1️⃣ **Mở Network của connections_blank**  
   - **Double-click** vào **connections_blank node** để mở biểu đồ bên trong.  
   - Tìm node có tên **all_connections**.  

2️⃣ **Mở all_connections Node**  
   - **Double-click** vào **all_connections node** để xem chi tiết network của nó.  
   - Đây là nơi xử lý tất cả các kết nối giữa đường cao tốc và đường thành phố.  

✅ **Bước tiếp theo:** Chỉnh sửa **all_connections** để tối ưu hóa điểm vào/ra của Freeway! 🚦
![image](https://github.com/user-attachments/assets/7cec0cc0-bf95-4dc0-b84f-07ef4fc6bc3d)
- Trong **Network pane**, tìm **ROAD_REFERENCE node** trong biểu đồ của **all_connections**.  
- Nhấn **Display** (biểu tượng con mắt) để hiển thị nó trong Viewport.  

✅ **Giờ bạn có thể xem tham chiếu đường phố để căn chỉnh các kết nối của đường cao tốc!** 🚗💨
![image](https://github.com/user-attachments/assets/a9203f90-e7c7-4867-9ed1-61d36593ac1e)

- **Giữ Ctrl** và chọn cả **ROAD_REFERENCE** và **merge_freeway** nodes.  
- Nhấn **Display Template** (biểu tượng màu hồng) trên cả hai nodes để hiển thị chúng trong Viewport.  

✅ **Bây giờ bạn có thể xem tham chiếu đường và cách đường cao tốc kết nối với thành phố!** 🚦🏙️

![image](https://github.com/user-attachments/assets/2c7d7093-e9f4-48da-9f17-91c3fea3c6d2)

- Trong **graph**, chọn **connection_set_1** node.  
- Trong **cửa sổ thuộc tính**, bật **Preview Mode** để có phản hồi nhanh hơn khi chỉnh sửa.  

✅ **Bây giờ bạn có thể chỉnh sửa kết nối đường cao tốc với thành phố một cách hiệu quả hơn!** 🚀🏙️
![image](https://github.com/user-attachments/assets/8da2ca12-f5ee-4825-b1ed-1cb21d70d3be)
- Trong **cửa sổ thuộc tính**, nhấp vào **dấu cộng (+)** bên cạnh thuộc tính **Connections**.  
- Hành động này sẽ thêm một **curve** để kết nối đường cao tốc với một con đường trong thành phố.  

✅ **Bây giờ bạn có thể điều chỉnh đường kết nối theo ý muốn!** 🚗🏙️
![image](https://github.com/user-attachments/assets/322e1c8d-a095-4f7b-9c7e-27a414afdf0c)

- Trong **cửa sổ thuộc tính**, nhấp vào **Edit Curve 0** để chỉnh sửa đường cong kết nối.  
- Sau khi nhấp, bạn có thể di chuyển các điểm của đường cong để tinh chỉnh kết nối giữa đường cao tốc và đường trong thành phố.  

✅ **Tiếp tục điều chỉnh để đảm bảo kết nối mượt mà!** 🚗🏙️

![image](https://github.com/user-attachments/assets/45958582-c14e-4ce6-ad96-dd8f63c026c2)

- **Bật công cụ Handle** (phím tắt: **Enter** khi ở chế độ chỉnh sửa).  
- Nhấp vào hai điểm:  
  - **Một điểm gần đường cao tốc**.  
  - **Một điểm trên con đường trong thành phố** mà bạn muốn kết nối.  
- **Chỉnh sửa điểm:**  
  - **Giữ Ctrl + nhấp chuột trái** để điều chỉnh điểm kết nối trên đường phố.  
  - **Giữ Shift + nhấp chuột trái** để điều chỉnh điểm kết nối trên đường cao tốc.  

🔧 **Tùy chỉnh đường cong để đảm bảo kết nối trơn tru và tự nhiên!** 🚧🚗

![image](https://github.com/user-attachments/assets/ed7a3f72-bd38-4f79-a284-0fa7d1702c0c)
Khi nhấp vào điểm cuối cùng để hoàn tất kết nối, bạn sẽ thấy đường cong kết nối giữa đường cao tốc và đường phố xuất hiện trong Viewport. Nếu cần, bạn có thể tiếp tục điều chỉnh các điểm để đảm bảo đường cong trơn tru và phù hợp với dòng giao thông trong thành phố. 🚗🏙️

![image](https://github.com/user-attachments/assets/2e6d3d56-2874-45d9-897b-a097730024c5)
Sau khi hoàn thành các kết nối cần thiết giữa đường cao tốc và đường phố, hãy chọn node `connection_set_1` trong graph và tắt **Preview Mode** trong cửa sổ thuộc tính.  

Bạn cũng có thể tinh chỉnh cách đường cao tốc kết nối với đường bên dưới bằng cách điều chỉnh các thuộc tính như:  
- **Interpolation:** Kiểm soát độ cong của đường kết nối.  
- **Elevation:** Điều chỉnh độ cao của đoạn đường nối.  
- **Banking:** Thay đổi độ nghiêng của đường để đảm bảo chuyển động mượt mà hơn.  
![image](https://github.com/user-attachments/assets/2cf042e1-3575-4a21-8f8c-1ab8e0e0c0ab)
Sau khi mở node **City Processor**, bạn sẽ thấy phần **3. LOTS** (màu cam) trong graph. Tại đây, hãy tìm và chọn node **City_Lot_Processor** (vòng tròn màu vàng).  

Node này cho phép bạn điều chỉnh nhiều thuộc tính quan trọng, bao gồm:  
- **Kích thước lô đất**: Xác định diện tích mặt bằng cho từng tòa nhà.  
- **Setbacks (khoảng lùi)**: Điều chỉnh không gian vỉa hè hoặc khoảng cách giữa các công trình.  
- **Phong cách kiến trúc**: Chọn các kiểu nhà khác nhau để tạo sự đa dạng.  
- **Biến thể hình dạng**: Điều chỉnh độ cao, kiểu dáng của các tòa nhà để tránh sự lặp lại đơn điệu.  

![image](https://github.com/user-attachments/assets/ce57cf92-d10d-46b8-bb8a-2b32f905bd8a)

Khi đã chọn node **City_Lot_Processor**, hãy nhìn vào **properties pane** (bảng thuộc tính), nơi bạn có thể thấy hai tab chính:  

1. **LOTS tab** – Điều chỉnh các thuộc tính của lô đất, bao gồm:  
   - **Lot Size**: Kiểm soát kích thước lô đất.  
   - **Setbacks**: Xác định khoảng lùi giữa đường và công trình.  
   - **Lot Coverage**: Điều chỉnh mật độ xây dựng trên mỗi lô.  

2. **BUILDINGS tab** – Xác định các đặc điểm của tòa nhà, như:  
   - **Height Range**: Đặt giới hạn chiều cao tối thiểu và tối đa.  
   - **Building Styles**: Chọn kiểu dáng kiến trúc.  
   - **Variability**: Tạo sự đa dạng về hình dạng và kích thước.  

Hãy thử thay đổi các thông số này để tạo một thành phố có diện mạo phù hợp với phong cách mong muốn! 🏙️🚀

![image](https://github.com/user-attachments/assets/80cbfa09-d8b4-4425-b546-a163ef729ef3)
Bạn có thể sử dụng **City_Lot_Processor** để tinh chỉnh cách các lô đất và tòa nhà được tạo ra. Dưới đây là một số điều chỉnh quan trọng:  

### **Lô đất (LOTS tab)**  
- **Lot Size**: Kiểm soát kích thước của từng lô đất.  
- **Removal Distance from Freeway**: Đảm bảo các lô đất không quá gần đường cao tốc.  
- **Sidewalk Consideration**: Điều chỉnh khoảng lùi để dành không gian cho vỉa hè.  

### **Tòa nhà (BUILDINGS tab)**  
- **Building Style**: Chọn kiểu dáng kiến trúc của tòa nhà (hiện đại, cổ điển, v.v.).  
- **Height & Size**: Định nghĩa chiều cao tối thiểu, tối đa và kích thước tổng thể.  
- **Variability**: Tăng độ ngẫu nhiên để thành phố trông tự nhiên hơn.  

![image](https://github.com/user-attachments/assets/9ffc3707-83bd-44f5-8bae-c6ffad48c251)

### **Bước 11 - Tạo Cache Thành Phố và Xuất Dữ Liệu**  

Ở bước cuối cùng này, bạn sẽ sử dụng **City Processor** để tạo cache và xuất dữ liệu, giúp nhập thành phố vào **Unreal Engine 5**.  

#### **1️⃣ Chuyển Houdini sang Manual Mode**  
- Điều này giúp ngăn Houdini tự động cập nhật khi bạn điều chỉnh **City Processor**, giúp tiết kiệm tài nguyên.  

#### **2️⃣ Cấu hình City Processor**  
- **Bật Procedural Dependency Graph (PDG)** nếu bạn muốn xử lý từng phần riêng lẻ.  
- Điều chỉnh **các tùy chọn xử lý** phù hợp với quy mô và yêu cầu của dự án.  

#### **3️⃣ Xuất dữ liệu thành phố**  
- Kiểm tra lại bố cục và các thông số.  
- Xuất dữ liệu ở định dạng **USD, FBX hoặc HDA** để sử dụng trong **Unreal Engine 5**.  

![image](https://github.com/user-attachments/assets/4302d661-15e0-4c23-ac93-2fe901a0babe)
### **Tạo Cache Thành Phố và Xuất Dữ Liệu**  

#### **1️⃣ Chọn City Processor**  
- Trong **Network Pane**, chọn **City Processor Node**.  

#### **2️⃣ Bật hoặc Tắt PDG**  
- Trong **City Processor Properties**, tìm tùy chọn **Use PDG**.  
- **Bật** nếu muốn sử dụng **Procedural Dependency Graph (PDG)** để tối ưu hóa xử lý.  
- **Tắt** nếu muốn xử lý theo cách thủ công.  

#### **3️⃣ Xác nhận cấu hình trước khi xuất**  
- Kiểm tra lại bố cục, kết nối đường phố và các vùng thành phố.  
- Chọn **định dạng xuất dữ liệu** (USD, FBX, HDA).  

Sau khi hoàn tất, bạn có thể tiếp tục với bước **xuất dữ liệu và nhập vào Unreal Engine 5** để hoàn thiện thành phố của mình! 🏙️🚀
![image](https://github.com/user-attachments/assets/d1c62244-730c-4f4a-af9c-4ffcf3177657)
### **Sử dụng PDG để Cải Thiện Hiệu Suất Xử Lý Thành Phố**  

#### **1️⃣ PDG và Tốc Độ Xử Lý**  
PDG (**Procedural Dependency Graph**) giúp **tăng tốc xử lý**, đặc biệt khi thành phố lớn. Nó cho phép **chạy song song nhiều tác vụ**, giúp tạo thành phố nhanh hơn.

#### **2️⃣ Các Bước Xử Lý trong PDG**  
Khi bật **Use PDG**, bạn cần thực hiện **ba bước xử lý chính**:  
✅ **Process City Base** – Xử lý địa hình và cấu trúc cơ bản.  
✅ **PDG Process** – Xử lý song song dữ liệu thành phố.  
✅ **Process City Furniture** – Xử lý vật thể nhỏ như đèn đường, cây cối.  

#### **3️⃣ Khi Nào Nên Dùng PDG?**  
- **Nên bật** nếu bạn có **máy mạnh** và thành phố lớn.  
- **Nên tắt** nếu bạn làm thành phố nhỏ hoặc muốn kiểm soát từng bước thủ công.  

Khi hoàn tất, **chạy PDG** để tối ưu hóa tốc độ tạo thành phố! 🚀
![image](https://github.com/user-attachments/assets/0ff9c0c0-b922-4458-8fec-59c54b8ddd6c)
### **Xử Lý Thành Phố Không Dùng PDG**  

Nếu bạn không sử dụng **PDG**, hãy nhấp vào **"Process City Without PDG"** để tạo các bộ nhớ cache (**caches**) cần thiết.  

#### **🔹 Điều Gì Xảy Ra Khi Xử Lý Không Dùng PDG?**  
- **Houdini sẽ xử lý tuần tự** từng phần của thành phố.  
- **Không tận dụng đa luồng**, dẫn đến **tốc độ chậm hơn**, đặc biệt với thành phố lớn.  
- **Dễ kiểm soát hơn**, thích hợp khi cần điều chỉnh từng bước thủ công.  

#### **🔹 Khi Nào Nên Xử Lý Không Dùng PDG?**  
✅ Khi bạn muốn **kiểm tra từng giai đoạn** trước khi xuất dữ liệu.  
✅ Khi **máy không đủ mạnh** để chạy nhiều luồng cùng lúc.  
✅ Khi **cần debug lỗi** trong quá trình sinh procedural.  

Sau khi hoàn thành, bạn có thể **xuất dữ liệu** để nhập vào **Unreal Engine 5**! 🚀
![image](https://github.com/user-attachments/assets/97a3f3d4-2d4b-4672-8800-b81e66cdc6f4)
### **Xuất Dữ Liệu Sau Khi Xử Lý Thành Phố**  

Sau khi quá trình xử lý hoàn tất, hãy thực hiện các bước sau tùy thuộc vào trạng thái của **"Use PDG"**:  

---

### **🔹 Nếu "Use PDG" Được Bật:**  
✅ Nhấn vào **"EXPORT ALL PBC"** để xuất:  
- **Hình học của thành phố** (geometry).  
- **Point Cloud Alembics (PBC)** – dữ liệu đám mây điểm giúp tối ưu hiển thị trong Unreal Engine 5.  

---

### **🔹 Nếu "Use PDG" Bị Tắt:**  
✅ Nhấn vào **"EXPORT CITY DATA"** để xuất dữ liệu thành phố mà không dùng PDG.  

📌 **Lưu ý:**  
- **PBC giúp tối ưu hóa việc hiển thị** trong UE5 bằng cách nén dữ liệu thành phố.  
- **Tốc độ xuất có thể lâu hơn nếu không dùng PDG**, đặc biệt với thành phố lớn.  

Sau khi hoàn tất, bạn có thể **nhập dữ liệu vào Unreal Engine 5** và tiếp tục tinh chỉnh thành phố của mình! 🚀
![image](https://github.com/user-attachments/assets/ed463b62-a5a1-4236-b988-a9bbf98bf831)

### **Xuất Dữ Liệu Khi "Use PDG" Bị Tắt**  

Nếu **"Use PDG" bị tắt**, thực hiện các bước sau để đảm bảo dữ liệu thành phố được xuất đúng cách:  

1️⃣ **Mở tab "Caches and Exports"** trong cửa sổ thuộc tính của **City Processor**.  
2️⃣ **Kiểm tra rằng dữ liệu được đọc từ ổ đĩa** để tránh tính toán lại không cần thiết.  
3️⃣ **Trong phần "Geometry and PBC Export" ở cuối tab**, nhấn **"EXPORT ALL PBC"** để xuất:  
   - **Dữ liệu hình học (Geometry)** của thành phố.  
   - **Point Cloud Alembics (PBC)** để tối ưu hóa hiển thị trong Unreal Engine 5.  

📌 **Lưu ý:**  
- Việc xuất PBC giúp giảm tải hiệu suất khi nhập thành phố vào UE5.  
- Nếu dữ liệu không xuất đúng cách, hãy đảm bảo **các bộ nhớ đệm (caches) đã được cập nhật** trước khi xuất.  

Sau khi hoàn tất, bạn có thể **nhập dữ liệu vào Unreal Engine 5** để tiếp tục chỉnh sửa! 🚀
![image](https://github.com/user-attachments/assets/c395a868-938b-4556-b6fb-919ae510abe6)
### **Hoàn Thành Xuất Dữ Liệu Thành Phố 🎉**  

Bạn đã hoàn tất quá trình xử lý và xuất tất cả dữ liệu cần thiết từ Houdini! 🎊  

🛠 **Bước Tiếp Theo:**  
Bây giờ, bạn có thể **chuyển sang phần thứ hai của hướng dẫn**, trong đó bạn sẽ **nhập dữ liệu thành phố từ Houdini vào Unreal Engine 5** bằng cách sử dụng **City Sample project**.  

📌 **Tiếp tục với:**  
➡ **City Sample: Generating a City and Freeway in Unreal Engine 5**  
➡ Hoàn thiện quá trình phát triển thành phố trong Unreal Engine  
➡ Trải nghiệm toàn bộ thành phố của bạn với hệ thống đường phố và cao tốc đã thiết lập  

🚀 **Sẵn sàng đưa thành phố của bạn vào UE5? Hãy tiếp tục thôi!**
![image](https://github.com/user-attachments/assets/9f72f36c-6c4e-4957-94d9-736ad3990517)
































