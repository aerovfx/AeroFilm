**best practices** (thực hành tốt) khi làm việc với **OTL** (Operator Type Library) hoặc HDA (Houdini Digital Asset) trong Houdini. Cụ thể:

1. **Ask before creating a new OTL**  
   - Khuyến nghị bạn nên **thảo luận** với nhóm hoặc kiểm tra thư viện OTL/HDA hiện có **trước khi** tạo một OTL/HDA mới.  
   - Mục đích:  
     - Tránh trùng lặp (duplicate) các OTL có chức năng tương tự.  
     - Tiết kiệm thời gian và công sức bảo trì, vì có thể đã có một OTL đáp ứng nhu cầu.

2. **Save big changes as a new version**  
   - Mỗi khi có thay đổi lớn (chẳng hạn chỉnh sửa logic, thêm nhiều tham số, thay đổi kết cấu quan trọng), nên **lưu** thành **một phiên bản mới** của OTL/HDA.  
   - Mục đích:  
     - **Version control**: Dễ dàng quay lại phiên bản cũ nếu có lỗi.  
     - Giúp đồng đội và pipeline **theo dõi** sự thay đổi, tránh xung đột khi nhiều người sử dụng cùng một OTL.

3. **Modular OTLs are always better**  
   - Khuyến khích thiết kế OTL/HDA một cách **modular**, nghĩa là mỗi OTL làm **một nhiệm vụ cụ thể**.  
   - Mục đích:  
     - Dễ bảo trì và nâng cấp.  
     - Tái sử dụng (reuse) dễ dàng hơn khi chia nhỏ chức năng.  
     - Giảm rủi ro khi một OTL quá phức tạp, khó quản lý.

4. **Only expose the parameters needed**  
   - Khi tạo OTL/HDA, chỉ nên **công khai** (expose) những tham số **thực sự cần** cho người dùng (artist, technical director, v.v.).  
   - Mục đích:  
     - Giao diện gọn gàng, dễ sử dụng.  
     - Giảm nhầm lẫn, tránh lộ các tham số nội bộ không cần thiết.  
     - Giữ cho OTL/HDA **trực quan** và **dễ tiếp cận** hơn.

---

### Tổng kết
Các nguyên tắc trên hướng tới một **quy trình làm việc tối ưu** khi phát triển và sử dụng OTL/HDA trong dự án. Việc **thảo luận trước** khi tạo mới, **phiên bản hoá** thay đổi, giữ cho OTL **modular**, và **giới hạn** tham số công khai sẽ giúp bạn duy trì **tính ổn định**, **tái sử dụng**, và **dễ bảo trì** của toàn bộ hệ thống.
