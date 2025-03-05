---

## **1. Density (Mật độ)**
- **Hiện tại**: 3  
- **Đề xuất**: **2** hoặc **1**  
- **Giải thích**: Giá trị này càng cao, mạng lưới đường phố càng dày đặc, dẫn đến nhiều block hơn (tương ứng nhiều tòa nhà hơn). Giảm **density** sẽ hạn chế số lượng block, giúp thành phố nhỏ và ít tòa nhà hơn.

---

## **2. Shallow Angle Roads**
- **Enable**: đang bật (✓)  
- **Angle**: 11.92 (có thể thay đổi)  
- **Giải thích**:  
  - **Angle** quyết định độ nghiêng của các đường “xiên” so với đường chính.  
  - **Gợi ý**: Giữ khoảng 10–15° để tạo một chút chênh lệch, tránh thành phố quá vuông vức. Nếu bạn muốn đường phố vuông góc, có thể giảm góc về gần 0 (hoặc dùng Road Network Sizes để tạo ô vuông).

---

## **3. Max Block Length (X/Z)**
- **Hiện tại**: X = 100, Z = 150  
- **Đề xuất**: **Tăng giá trị** (ví dụ X = 200, Z = 200)  
- **Giải thích**:  
  - Đây là **kích thước tối đa** của mỗi block.  
  - Block càng lớn → **ít block** hơn trong cùng một khu vực → **ít tòa nhà** hơn.  
  - Nếu bạn muốn đường phố ngắn và chia nhỏ, hãy giảm giá trị này. Nếu muốn ít block và ít tòa nhà, hãy **tăng** nó.

---

## **4. Offset**
- **Hiện tại**: -86.2, 0, -80.4 (có vẻ là 3 giá trị cho X, Y, Z hoặc tương tự)  
- **Giải thích**:  
  - Offset thường để dịch chuyển vị trí ban đầu của đường so với hệ trục.  
  - Thông số này không trực tiếp giảm số lượng block/tòa nhà, mà chỉ thay đổi vị trí đường.  
  - Giữ nguyên hoặc tinh chỉnh để bố cục thành phố phù hợp với cảnh quan của bạn.

---

## **5. Road Creation Threshold**
- **Hiện tại**: 0.189  
- **Đề xuất**: **Tăng nhẹ** (ví dụ 0.3 – 0.5)  
- **Giải thích**:  
  - Thông số này (nếu đúng như tên gọi) quyết định “ngưỡng” để tạo đường mới.  
  - Giá trị cao hơn thường **khó tạo đường** hơn, dẫn đến **ít đường** → ít block → ít tòa nhà.  
  - Tuy nhiên, cần thử nghiệm vì tùy phiên bản công cụ, ý nghĩa chính xác có thể khác nhau.

---

## **6. Minimum Distance to Freeway**
- **Hiện tại**: 150  
- **Đề xuất**: Tăng lên **200** (hoặc hơn) nếu bạn muốn giữ đường nội bộ cách xa freeway.  
- **Giải thích**:  
  - Xác định khoảng cách tối thiểu từ đường phố đến đường cao tốc.  
  - Tăng giá trị này có thể làm một số đường phố không được sinh ra gần freeway, **giảm** tổng số đường.

---

## **Tóm Tắt Cách Tạo Thành Phố Nhỏ & Ít Nhà**
1. **Giảm Road Density** (từ 3 xuống 2 hoặc 1).  
2. **Tăng Max Block Length** để mỗi block to hơn, số block giảm.  
3. **Tăng Road Creation Threshold** (nếu muốn đường phố khan hiếm hơn).  
4. **Giới hạn chiều cao tòa nhà** hoặc **giảm Building Coverage** (nếu có tùy chọn) để có ít công trình hơn.  

Bằng cách phối hợp các thay đổi này, bạn sẽ tạo được một **thành phố nhỏ gọn**, ít đường, ít block, và do đó **giảm số lượng tòa nhà** tổng thể. Hãy điều chỉnh từng tham số từ từ và quan sát kết quả trong Viewport để đạt được layout ưng ý nhất. Chúc bạn thành công!
