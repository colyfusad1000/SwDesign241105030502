# Phân tích hệ thống Payroll System


## 1. Kiến trúc đề xuất:

Kiến trúc 3 lớp là một trong những kiến trúc phổ biến và hiệu quả cho các hệ thống lớn như hệ thống tính lương (Payroll System). Kiến trúc này giúp phân tách rõ ràng giữa các thành phần, đảm bảo tính linh hoạt, bảo trì dễ dàng và khả năng mở rộng cao.

Các tầng trong hệ thống:
  - Lớp Giao Diện (Presentation Layer): Đây là lớp hiển thị thông tin và tương tác với người dùng. Nó nhận yêu cầu từ người dùng, chuyển dữ liệu đến các lớp phía sau để xử lý, và hiển thị kết quả.
  - Lớp Xử Lý Nghiệp Vụ (Business Logic Layer): Lớp này chứa các logic nghiệp vụ và quy tắc xử lý cốt lõi của hệ thống. Nhiệm vụ của nó là xử lý dữ liệu, tính toán và điều hướng các yêu cầu từ lớp giao diện.
  - Lớp Dữ Liệu (Data Access Layer): Lớp này chịu trách nhiệm truy cập, lưu trữ và quản lý dữ liệu trong cơ sở dữ liệu. Nó xử lý các thao tác CRUD (Create, Read, Update, Delete) và cung cấp dữ liệu cho lớp xử lý nghiệp vụ.
    
Giải thích:
  - Kiến trúc phân lớp cho phép phân tách các mối quan tâm, dễ bảo trì và mở rộng. Kiến trúc này có thể mở rộng thêm các dịch vụ khác mà không ảnh hưởng đến các phần còn lại.
  - Kiến trúc 3 tầng cho phép tách biệt rõ ràng giữa giao diện, xử lý nghiệp vụ và lưu trữ dữ liệu. Điều này giúp tăng tính modular, dễ bảo trì và phát triển.
  - Các lớp được tách biệt giúp bảo vệ dữ liệu quan trọng, giảm rủi ro bảo mật bằng cách hạn chế quyền truy cập trực tiếp đến cơ sở dữ liệu.
  - Có thể dễ dàng thay đổi logic nghiệp vụ hoặc giao diện mà không ảnh hưởng đến dữ liệu, và ngược lại.
  - Với kiến trúc phân lớp, các thành viên trong nhóm phát triển có thể tập trung vào các phần riêng biệt mà không ảnh hưởng đến nhau. 

![Diagram](https://www.planttext.com/api/plantuml/png/b9BFIWCn48VlUOfXxprvBKjf5pouY60HFGwx8HkQ9al-K8fuzY74etWgUdM3zB3WU-G9V0MpLTh2weAtC9dlzqs6VFhjn5ZKrYq5CGikQzIu14qBYv892hS4O8h5WcdbP3bJGcd8EQli3HL2hUBjPOMbMd79m6f7oHqXbjj8dl7GR6Kijaq19o22VwW9EIGdyz0yH-gKeuAC1tylavtkg6Ky5hYcEasFk-2SVRm6_yWXQzyaIm0DN6XggBHekP9vXtHpz5tNmMyWRzzZHDLbrN0L_DE0zYyWAgVES4cDoHNZnO0p2_ubhYp2Ra0qrsuDiz1iwcz0_01HbA75VNxleJ0QfR_DqY_jEWzXP7_yPqH_rnCgo-u3VG400F__0m00)

## 2. Cơ chế phân tích

Các cơ chế phân tích giúp giải quyết các vấn đề phức tạp trong hệ thống. Một số cơ chế phân tích có thể áp dụng cho Payroll System là:
  - Persistency: Đảm bảo rằng thông tin về nhân viên, thanh toán, và thời gian làm việc được lưu trữ an toàn, giúp hệ thống có thể phục hồi và truy xuất dữ liệu khi cần thiết.
  - Communication (IPC and RPC): Cần thiết để các thành phần trong hệ thống có thể trao đổi dữ liệu một cách hiệu quả và chính xác, đảm bảo tính liên kết giữa các phần của hệ thống.
  - Transaction Management: Quản lý giao dịch để đảm bảo tính nhất quán trong quá trình thanh toán. Đảm bảo tính toàn vẹn của dữ liệu, đặc biệt trong các tình huống giao dịch phức tạp, như khi tính toán lương và ghi nhận thời gian làm việc.
  - Security: Đảm bảo thông tin nhân viên và các thanh toán được lưu trữ an toàn, chỉ có quyền truy cập từ những người có thẩm quyền. Đặc biệt quan trọng trong hệ thống tính lương, nơi chứa nhiều thông tin cá nhân và tài chính của nhân viên.
  - Error Handling: Quản lý các lỗi phát sinh khi giao dịch không thành công. Giúp nâng cao độ tin cậy của hệ thống và cung cấp thông tin cần thiết để sửa chữa lỗi một cách nhanh chóng.
  - Legacy interface: Đảm bảo rằng hệ thống mới có thể làm việc hiệu quả với các hệ thống cũ mà không gặp khó khăn, giúp giảm thiểu chi phí chuyển đổi và thời gian gián đoạn.

## 3. Phân tích ca sử dụng Select Payment
1. Biểu đồ tuần tự
   
![Sequence Diagram](https://www.planttext.com/api/plantuml/png/Z99DJiCm48NtFiN86q222tI1ke0bg2BY05DxA5RzXpr1ojbOS2IkmBX9Q2aLi8fZpVlUcvTylBqlAsFXFdY5XbE1sv1z6eXKbcjdNCR8eBkXCWKDM64yAiMEFK57Bpr5Gt3ZS5Cmm9CmT4UU3CCAXq2HDTmHFoUhr0o7g-k9iu27HgWCdA2EiZpA88ogSR19Pla2LYM5p3kpxzDmhhCpM-YplWGTqFdsjAuqiAMSgcDzSJh9cBeU-olqqi1CdMy1JkMwJu3MEdOfeWSN9M30zWP5rfGKWYDVQOhsE-nWoJRjugR12zKgWbCBYE3LMQe_nYVFenh-xRx6k1KL2_LFwzrin420qG8QatgfClPXJKLoH2bWxpQh7xD5fY_msVuR75Iebg9kF-ed0000__y30000)

Nhiệm Vụ của Từng Lớp Phân Tích
- Employee (Actor): Đây là người dùng chính, là nhân viên chọn phương thức thanh toán.
- System (Participant): Đây là hệ thống xử lý thông tin và lưu trữ phương thức thanh toán của nhân viên.

2. Biểu đồ lớp
   
![Class Diagram](https://www.planttext.com/api/plantuml/png/T9B1JeGm48RlFCLaJsmY1w_4c5qN3aHPYOldJHScQoCjf1rCYFfa7dmaNy4kMP52zzHs-itCtt_wy_MzqiGKjQBoYeff3R5eghf3X7SF801UXi0bzNl918Qm8yNbiGyqh1CeAKLwgGsNZOy60D1OOK5Mt1SkEkyQN8RmLlFI-_JEKYpYh4SCkAD2t_E8524nNcb_EQWrDL6sOfxIbysIpVt-EJExT9qyc2LAdk9Dle_Yx76NvF-AKbFMgSh4JPjrMIhKUkJHoG9AhLkVsTJisH5NnhG8crfpSdKxCFcwdSw25KNTIjgsue1ggk3EPFoPCis-SgUEP0rVOd6zW23e5tlMjigR3mFDh791bvyweOFWrZ7k5Shoz7D_0G00__y30000)

Giải Thích Biểu Đồ Lớp
- Lớp Employee: Đại diện cho nhân viên, với các thuộc tính như id, name, và paymentMethod (phương thức thanh toán). Phương thức selectPaymentMethod cho phép nhân viên chọn phương thức thanh toán.
- Lớp PaymentMethod (Lớp): Đây là lớp cha chung cho các phương thức thanh toán. Thuộc tính methodType xác định loại phương thức và phương thức getDetails để lấy thông tin về phương thức thanh toán.
- PaymentMethodType (Enum): Liệt kê các loại phương thức thanh toán: PICK_UP, MAIL, và DIRECT_DEPOSIT.
- MailPaymentMethod (Lớp con của PaymentMethod): Đại diện cho phương thức nhận qua thư với thuộc tính mailingAddress.
- DirectDepositPaymentMethod (Lớp con của PaymentMethod): Đại diện cho phương thức chuyển khoản trực tiếp với thuộc tính bankName và accountNumber.
- **Trong đó**
  + 1 Employee có một PaymentMethod.
  + PaymentMethod là lớp cha của MailPaymentMethod và DirectDepositPaymentMethod, đại diện cho các phương thức thanh toán cụ thể.
  + PaymentMethod có liên kết với PaymentMethodType để xác định loại thanh toán.

## 4. Phân tích ca sử dụng Maintain Timecard
1. Biểu đồ tuần tự

![Sequence Diagram](https://www.planttext.com/api/plantuml/png/V5D9JiD04BpFArgvvmD8GK024X98Y23k7RiJ1irYfji1luq3J-8Bz7Z1YLbyiEHHLNLLJ_dp_UEC1PFKtXai92Quz9MB3P6fzDWMji8WC7kmdfQOIbWtBEHdW0mFo_Knw2x5Poe4RZ7WZZpfsGe5DyZK4kvkLyOi5d21R0kuSl4L5Wip38JvQPOyWNjwgOa5YZgbh37CDkZ63w0toy86z55M9Wz29x2oN3biHl1MWmro5IKRIqEEQGIKaHX2b4xsTzLb8XG230hl1mHw7UrHA8tfMHer1v5aQQ-KFLg76qTGF67Q4OJQRoYnKHZCXzmtEXdYTehviP_B89JWATQ9MpDCBczzGkkDj8n7TBRCtYbJgUp8Hv0rxW_NeTVMNjMwtdXxiFK_Bsq2FDOc0MsPr0mIOTP1XShPxoRxP3kqGHVYh8A_lHxSHWnRc_neZRCiiusXTNxkD6f0iPfhS9qBT1tsUL2_fxplRXd_5ebIqWPvOjPYJwg3JdjHDjty7Ej_gGoUn-2QIN7Ez9t_mYy0003__mC0)

Nhiệm Vụ của Từng Lớp Phân Tích
- Employee: Đại diện cho nhân viên, người sử dụng hệ thống để cập nhật và nộp bản chấm công.
- TCS (TimeCard System): Hệ thống chấm công, quản lý tất cả các yêu cầu từ nhân viên và xử lý chấm công.
- PMD (Project Management Database): Cơ sở dữ liệu quản lý dự án, cung cấp danh sách số tham chiếu khi nhân viên chọn dự án mà mình đã làm.

2. Biểu đồ lớp
   
![Class Diagram](https://www.planttext.com/api/plantuml/png/T9BDIiGm4CVlUOhGaufxyBf8MTaL55mHL_0W7gRja8tceoIJWeXFvi57yXLClqAxhBaayy_mc_zCyllzi_84Ze9Mh5JWFR_MjR8VYFoJyNRX4DzMIxuZ9uteTGCQvueFXPRq93MkmLKdf-oB3SnH6vaqn8VC2WWVmOW8tiJZosilxsrm_jcwTupvMwWlrtjm0k-3Bj2TyuqDXS9yC450mS-n3IZPeczQJlJL9oBjkjmaG8DJqzCYet7JHGUcqPTErYIjIHS9yk3i6vQq1GC2DHgAVK41FerN85qr81N45gOLewqblvEUPitcBJczK7QHySKYx_Pnn2pDEjsUPRDUZcJ4_L-ZZAtGLEt_-0C00F__0m00)

Giải Thích Biểu Đồ Lớp
- Employee: Lớp đại diện cho nhân viên. Nhân viên có thể nộp bản chấm công thông qua phương thức submitTimeCard().
  + employeeId và name là các thuộc tính của nhân viên.
- TimeCard: Lớp đại diện cho bản chấm công. TimeCard chứa các thuộc tính như timeCardId, dateRange, hoursWorked, và status.
  + validateHours(): Phương thức kiểm tra tính hợp lệ của số giờ làm.
  + setStatus(): Phương thức đặt trạng thái cho TimeCard (ví dụ, "Submitted").
  + save(): Phương thức lưu thông tin bản chấm công vào hệ thống.
- ChargeNumber: Lớp đại diện cho số tham chiếu của dự án, chứa các thuộc tính number và description.
- ProjectManagementDatabase: Lớp đại diện cho cơ sở dữ liệu quản lý dự án, có phương thức getAvailableChargeNumbers() để lấy danh sách các số tham chiếu có sẵn.
- Quan hệ giữa các lớp:
  + Employee --> TimeCard: Một nhân viên có thể liên kết với một bản chấm công hiện tại.
  + TimeCard --> ChargeNumber: Mỗi bản chấm công có thể chứa nhiều số tham chiếu.
  + TimeCard --> ProjectManagementDatabase: Bản chấm công tương tác với cơ sở dữ liệu quản lý dự án để lấy danh sách số tham chiếu.

## 5. Hợp nhất kết quả phân tích

![Class Diagram](https://www.planttext.com/api/plantuml/png/T5HDJ-Cm4BtdLqGzPH4zx1MXYcvJYMW9LBHe3mYXIJ9AlSHsP4ygLR2_R0_y9Fu2Thweaz1B_F7cpSoRvtxyVx_I18egNdXf0LhxQruMyeZeltg-_M6xZx8BVqkAYRmv5y3HFIdXo55GZBIN1hmvtJO8ZGMcv5m4V0g-EvRuuy8_IDP5LWbdj6CSLw2oeBlxvxLLEz5jwNFUSqtGDxmvKeW4hD2Mi-t6iAAe-3Yc9Tv4gz_F3vjw7I-ZcteHHlVhrUuvN6_kjj7kgxBOa4zNPovCjcMMATJQbL8ZnSvr02vi9438b94sn59gHfFv4X0ljyEXpI5DPINejk89gb4HlqnCfyym_joVZ1rLrWsjCnIr-w6XCY2y1v6R1A5PFZurntjPAVr7gXSq-1ZAozKUL8vDqdC_b5LIuAAjc82gWPG7A9YblhOyWMigf6qT4RY1BWWEEFRRQH5TOs92mmnrgbX9J8fJUxMcLVAl6LeC0dAq0pDzGmAwVtl6dSk34HzCYwSPwpvkc2P7Z8Lbxf_lxEVCdy_hZ_iI1uX5_Us6vBdMkNmp52C7Ju6-zzy0RJEE7sDlahweivaZyWJ2TlQTWfvtXIAp_sgV0000__y30000)
