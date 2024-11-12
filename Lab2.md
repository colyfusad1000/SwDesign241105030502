# Phân tích ca sử dụng Create Administrative Report
1. Mô tả

Ca sử dụng này cho phép Payroll Administrator (Quản trị viên bảng lương) tạo báo cáo "Tổng số giờ làm việc" hoặc "Tiền lương tính đến nay trong năm".

2. Biểu đồ tuần tự

![Sequence Diagram 'Create Administrative Report'](https://www.planttext.com/api/plantuml/png/d5HBJiCm4Dtd5BC4gLmW2rHK9CG6LOrO8HOZUm1BZctiQL7Ene8ZSGKSuX0J3AND8eaoypxpFChxwzioC7hUjhf2mTR36ZjljRwGhJ8giCVuiNAnHGdbq31io5dF6thUKk3Rwq9jPGtt75G2DkHtIb2XKbKbRJWxdqlMa5w1BGXFo0H-e9Xrzk0IwSGmu2ABOl8AuOGxHmkGaJCiW5gdRKSKJl_lRUtjJacQCvUipUEgeI4ZVq5ERHCqXLd35HdoFt98vQc_XbKU5xmeVW8t69PpmOBCXdZh3JmcDRb7BfyiGRy1IYDbILwgu3Hs8wP2pN3Nu8w6pliAudNCpeJ8CRBs70TlZS6M0EDHQIkGbJM7MHbNf4pp_qN9veYFp_wCuS-5QJ9eduWZeHuKPLQYG8eydeD0BuzA_UOhxRczFGCcqV6OUZVBUEj_L1y0003__mC0)

**Giải thích**

PayrollAdministrator (PA)
  - Request to create report: PA yêu cầu hệ thống tạo một báo cáo.
  - Provide report criteria: Cung cấp các thông tin cần thiết để tạo báo cáo, bao gồm loại báo cáo, ngày bắt đầu, ngày kết thúc, và tên nhân viên.
  - Request to save report (nếu có): Nếu chọn lưu báo cáo, PA yêu cầu hệ thống lưu báo cáo, đồng thời cung cấp tên và vị trí để lưu.
  - No save request (nếu không lưu): PA không thực hiện yêu cầu lưu báo cáo nếu quyết định không lưu.

ReportRequestUI (UI)
  - Request report criteria: Hiển thị biểu mẫu và yêu cầu PA cung cấp các tiêu chí cần thiết để tạo báo cáo.
  - Send report criteria: Gửi các tiêu chí báo cáo đã nhận được từ PA tới ReportController để xử lý việc tạo báo cáo.
  - Display report: Hiển thị báo cáo đã được tạo cho PA xem.
  - Request name and location (khi lưu báo cáo): Yêu cầu PA cung cấp tên và vị trí lưu báo cáo nếu PA chọn lưu.
  - Send save report request: Gửi yêu cầu lưu báo cáo tới ReportController với tên và vị trí mà PA đã cung cấp.
  - Discard report: Nếu PA không chọn lưu báo cáo, UI gửi lệnh hủy báo cáo tới ReportController.

ReportController (RC)
  - Send report criteria to ReportService: Nhận tiêu chí từ UI và gửi tới ReportService để bắt đầu quá trình tạo báo cáo.
  - Return report to UI: Sau khi báo cáo được tạo, nhận báo cáo từ ReportService và gửi lại cho UI để hiển thị cho PA.
  - Save report to ReportService: Khi nhận được yêu cầu lưu báo cáo từ UI, ReportController gửi yêu cầu này tới ReportService để thực hiện lưu báo cáo.
  - Discard report: Nếu không có yêu cầu lưu báo cáo, ReportController thực hiện việc hủy bỏ báo cáo theo yêu cầu từ UI.

ReportService (RS)
  - Generate report: Nhận tiêu chí từ ReportController và thực hiện việc tạo báo cáo, gửi yêu cầu tạo báo cáo tới lớp Report (entity).
  -Save report: Nhận yêu cầu lưu báo cáo từ ReportController và lưu báo cáo vào vị trí và tên được chỉ định bởi PA.
Report (R)
  - Create report: Nhận thông tin từ ReportService và tạo báo cáo theo các tiêu chí đã cung cấp (loại báo cáo, ngày tháng, danh sách nhân viên).
  - Return generated report: Trả báo cáo đã tạo lại cho ReportService.

3. Biểu đồ lớp

![Class Diagram 'Create Administrative Report'](https://www.planttext.com/api/plantuml/png/d5D1JiCm4Bpd5JucKli12rL51KIbgggW275SabK8TUnWRof5Y9Tnu4by0STssYHKbU0IUSVhsTcTpVVdrzmGQAfB4QK2Z66NMLd8EwoKfeSbUuyOor6Y1a8Fnec53EoxKAWKg52IitlIXSoJw2CAL3vZeGj2NO3ZqWxQDXLs-IrRg-3ALk2i_Le4PTQB3uGzRGibIIiXK0VUjneD3Il6mt0at4lXGUM4dMbaezKhfkGgLVwyp7eD16mDPR-j76dn0Zh7TLq-epPnmjcgC7JXCsP7_kko4gf1T0Km18CAf0Z4hQgrULHwX_RgHYWWUxC7B_iA6iFPKhQOATBT2cshVT1HRA1vGj1RvSVRaOmi_ktIP6pIPEXHqirnxFx_NMSi0uBHo8vItHxQ4TjSY9rNetMRJcT10sTf0AFXTjkCqol5kuKoqUc48_cX7cUrmNFvtHQrvBOTtADnBPvvSbYCFxm9S-Ui10cvLHJDxM3j3_u3003__mC0)

**Các lớp phân tích và nhiệm vụ của từng lớp**

AdminReportUI:
  - Nhiệm vụ: Đây là lớp giao diện, tương tác trực tiếp với người dùng để yêu cầu nhập tiêu chí báo cáo và khởi tạo yêu cầu tạo báo cáo từ AdminReportController. Lớp này cũng cho phép người dùng lưu báo cáo.
  - Phương thức:
    + generateReport(): Yêu cầu tạo báo cáo từ AdminReportController.
    + saveReport(location: String): Lưu báo cáo vào vị trí do người dùng chỉ định.

AdminReportController:
  - Nhiệm vụ: Đây là lớp điều khiển, chịu trách nhiệm quản lý quá trình tạo báo cáo, yêu cầu và lấy dữ liệu từ các lớp liên quan (như Employee và Project). Nó cũng xử lý logic lưu báo cáo.
  - Phương thức:
      + requestReport(criteria: ReportCriteria): Nhận yêu cầu từ AdminReportUI và tạo báo cáo dựa trên tiêu chí từ ReportCriteria.
      + saveReport(report: Report, location: String): Lưu báo cáo được tạo vào vị trí chỉ định.

Report:
  - Nhiệm vụ: Lớp này đại diện cho báo cáo thực tế, bao gồm các loại báo cáo khác nhau (như giờ làm, nghỉ phép, lương, v.v.) cùng các phương thức để tạo và lấy dữ liệu báo cáo.
  - Phương thức:
    + generate(): Tạo báo cáo dựa trên dữ liệu có sẵn và tiêu chí nhận được từ ReportCriteria.
    + getData(): Trả về dữ liệu báo cáo để hiển thị hoặc lưu.

ReportCriteria:
  - Nhiệm vụ: Lớp này lưu trữ tiêu chí báo cáo, chẳng hạn như loại báo cáo, ngày bắt đầu và kết thúc. Nó giúp AdminReportController có thể xác định rõ ràng thông tin cần để tạo báo cáo.
  - Thuộc tính: reportType, startDate, endDate.

Project:
  - Nhiệm vụ: Lớp này đại diện cho một dự án, bao gồm các thuộc tính liên quan đến mã số dự án và cung cấp danh sách các số mã (charge numbers) liên quan đến dự án để báo cáo về dự án.
  - Phương thức:
    + getChargeNumbers(): Cung cấp danh sách mã chi phí liên quan đến dự án nếu báo cáo yêu cầu dữ liệu về dự án.

Employee:
  - Nhiệm vụ: Đại diện cho nhân viên, bao gồm thông tin về thời gian làm việc, ngày nghỉ phép, tiền lương, và phương thức để tạo báo cáo dựa trên yêu cầu của AdminReportController.
  - Phương thức:
    + generateReport(reportType: String, startDate: Date, endDate: Date): Tạo báo cáo cho nhân viên dựa trên loại báo cáo và khoảng thời gian.
   
**Quan hệ giữa các lớp**
  - AdminReportUI — AdminReportController: AdminReportUI là giao diện người dùng sẽ gửi yêu cầu tạo báo cáo đến AdminReportController.
  - AdminReportController — Report: AdminReportController quản lý quá trình tạo báo cáo bằng cách lấy và cung cấp dữ liệu từ các lớp khác (như Employee và Project) dựa trên tiêu chí của ReportCriteria.
  - ReportCriteria — Report: ReportCriteria chứa thông tin về loại báo cáo và khoảng thời gian, được sử dụng trong lớp Report để tạo báo cáo chính xác.
  - AdminReportController — Project và Employee: AdminReportController truy vấn dữ liệu từ Project và Employee dựa trên loại báo cáo yêu cầu để tổng hợp thông tin cho báo cáo.

# Phân tích ca sử dụng Create Employee Report
1. Mô tả

Ca sử dụng cho phép Employee (Nhân viên) tạo báo cáo "Tổng số giờ làm việc", "Tổng số giờ làm việc cho một dự án", "Nghỉ phép/Nghỉ ốm" hoặc "Tổng lương tính đến nay".

2. Biểu đồ tuần tự

![Sequence Diagram 'Create Employee Report'](https://www.planttext.com/api/plantuml/png/Z5JDZjCm4BxxAKOzB-BU0rffGS05LXJ4UMfFn2oExRKdHNas3ZmIhu3jnjjGfL5wI9Fu-nb_CyxVtt_kas2KeRSgv7_M7D09lEk3zIEHElh16OmZVA7WetpxgBHt4hsTNZoSdon5HKvO6h0zFKR_H5gKKaqINhrv4Tl3eRZ3xY4I2htOJe2TQi12Qelx8je7WSv7Y1K0Eh9GPBpXaWadDjJGCWQwWxfnCDdt3iYPUgSKMfc85GQSOFVL2rhuu8UOuBkFFybKRsoxsod8ltcjr-7iyvldWP80df0j7Yr1E9D1UqDffd1X5QN9eWX8P3ejyIRCBMCPejleTediBQTWSLpWtMWasGARmpUaSYZ1fqhDeVv7pYjARM1VJy3jRUtXFJcAPT0cKcuvmX5JzlRkMc8rpfd0YkCyo3Px_dAubfFy78HpDHcOyDHAFG_cyj9rp8i7fUCySWvx0ioXMQ-nIAqqj9sP5UAsYP-L2hzOVbInrmj2opqxpEYrNsNtWJHtJ8lrB5UJxpkEVLCgHPaDn-2J5-x6IqI-WpHeJIbrWwqgYcoQVRcCfmJEdnrMMZC9jurnqXXDBgcE_Ns-va_oFm000F__0m00)

**Giải thích**

Employee (Nhân viên)
  - Tương tác với giao diện người dùng để khởi tạo yêu cầu tạo báo cáo, cung cấp các tiêu chí cho báo cáo, và chọn lưu báo cáo nếu cần.

ReportUI (Lớp giao diện người dùng)
  - Thu thập thông tin tiêu chí báo cáo từ nhân viên, bao gồm loại báo cáo, ngày bắt đầu, ngày kết thúc và mã dự án (nếu cần).
  - Hiển thị báo cáo cho nhân viên và cung cấp tùy chọn lưu báo cáo.
  - Xác nhận tên và vị trí lưu báo cáo khi nhân viên chọn lưu.

ReportController (Lớp xử lý)
  - Xử lý và điều phối quy trình tạo báo cáo.
  - Gửi yêu cầu đến lớp Project để lấy danh sách mã dự án nếu loại báo cáo cần mã dự án.
  - Gửi yêu cầu đến lớp Report để tạo báo cáo dựa trên tiêu chí được cung cấp và lưu trữ báo cáo nếu nhân viên chọn lưu.

Project (Lớp thực thể dự án)
  - Cung cấp danh sách mã dự án từ Cơ sở Dữ liệu Quản lý Dự án, để hỗ trợ việc tạo báo cáo "Total Hours Worked for a Project".

Report (Lớp thực thể báo cáo)
  - Tạo dữ liệu báo cáo dựa trên tiêu chí được cung cấp từ ReportController.
  - Lưu báo cáo đến tên và vị trí được chỉ định khi ReportController yêu cầu lưu.

3. Biểu đồ lớp

![Class Diagram 'Create Employee Report'](https://www.planttext.com/api/plantuml/png/R99BJiCm48RtEOMNi8ZOPu4gjO2oQ44y3Z34qyIIOnjxKXGXJiQ28t457CUfahYRoFdcuN_-yT_FxyOHMEfQcLKId6DthP6wHtn6eoszbUmhOond3YLMX7p4hxt1WhsG5QeEOQ5CHrih2As0MOGBPoJqOzMZ8Q6Lkxeks4aBxiEeVC5KDkEBiZF_pgB6aJ-WGWkaRPHeBqiBy-s0F1s-WQ7Y2rAFhN1r8OjZRnkmDHwwzXrjgcPoBCh0-5lk2cyB1QQWNOeosed1Z1ciaQPEfJhgz9vx8N4F2cgS9ZvwSbYt7k0JK3E33axfQDxZ2YnFFKvUG9xV9fQ7sVov8iS-1JNPEc4eEZjJ-ELyTEXyCWU2YydpyOeWsTr4ZIxkDjlunVcd-Wy00F__0m00)

**Các lớp phân tích và nhiệm vụ của từng lớp**

Employee
  - Nhiệm vụ: Lớp này đại diện cho nhân viên, cho phép truy xuất và quản lý thông tin về nhân viên.
  - Thuộc tính:
    + employeeID
    + name
    + position
Phương thức:
  - getEmployeeInfo(): Lấy thông tin nhân viên cho báo cáo.

ReportGenerator
  - Nhiệm vụ: Xử lý yêu cầu từ người dùng để tạo các loại báo cáo khác nhau.
  - Thuộc tính:
    + reportType
    + startDate
    + endDate
  - Phương thức:
    + generateReport(): Tạo báo cáo dựa trên tiêu chí được cung cấp.
    + selectChargeNumber(): Lựa chọn mã phí cho báo cáo dự án cụ thể.

EmployeeReportUI
  - Nhiệm vụ: Giao diện cho phép người dùng chọn loại báo cáo, nhập tiêu chí, và yêu cầu lưu báo cáo.
  - Thuộc tính:
    + selectedReportType
    + inputCriteria
  - Phương thức:
    + displayReportOptions(): Hiển thị các lựa chọn loại báo cáo.
    + enterCriteria(): Yêu cầu người dùng nhập tiêu chí báo cáo.
    + displayReport(): Hiển thị báo cáo đã tạo cho người dùng.

FileManager
  - Nhiệm vụ: Xử lý lưu trữ và xóa các báo cáo đã tạo.
  - Thuộc tính:
    + fileName
    + filePath
  - Phương thức:
    + saveReport(): Lưu báo cáo vào hệ thống.
    + discardReport(): Xóa báo cáo không lưu.

**Quan hệ giữa các lớp**
  - EmployeeReportUI tương tác với ReportGenerator để yêu cầu tạo báo cáo và lấy thông tin liên quan từ Employee.
  - ReportGenerator có thể yêu cầu Employee cung cấp thông tin nhân viên nếu cần thiết cho báo cáo.
  - ReportGenerator sau khi tạo báo cáo sẽ gửi kết quả tới EmployeeReportUI để hiển thị.
  - FileManager được EmployeeReportUI sử dụng để lưu hoặc xóa báo cáo sau khi người dùng xác nhận.

# Phân tích ca sử dụng Login
1. Mô tả

Ca sử dụng này cho phép người dùng có thể đăng nhập vào Payroll System

2. Biểu đồ tuần tự

![Sequence Diagram 'Login'](https://www.planttext.com/api/plantuml/png/R50n3i8m3Dpz2d-03tH0bO2D3S5kDLOLAN6Zs2tYRGmyYI-GKAfAW1VBPz_vxEVzqQfHjZ46eCw6Z6Vb3Ab0llE9nF1qK-C8K1kusNxg1WzY1HWBAXGPIHmcKhqEsLKfFv7nGfvJPLUL1YyKlAlzBhDZCKz1WOBXRgsHCkDK1m5Bh1ABWUFGlzUZ5-2W_4Fsyey-EzXxJO5ko3cNeoEhKi_0ui3nj_ksmEL1Bm000F__0m00)

3. Biểu đồ lớp

![Class Diagram 'Login'](https://www.planttext.com/api/plantuml/png/T59HIiH03FtlAVAvWht08Cik-2E8Y5qFCBPX7MYdooHr1V5aVdWahs0oRMTQN7zANvBtylBQdw_l7R4DF7HjKRUM29u90tmK02KCydhN672U4_QsGmCL1-UFiNWIqhaFpQeO-bQcdkHPV1QJiA99MDjBOSKFVuGnT8x8zPuCt3lYcyTKsMRPN9p4Cs-v8bTNYvBCVk1NzEngop9JONXpzMZNvWvkvWYkqzrN1bvwyM-zp1wHDR_Dc9oq5EKb5IwD4YQNYxELEl4Kull91QGz6xWL0mVNnKZZLohBxPXnZ5PH3YDFNBxChEugBWyfFJhvlpsVPA0Eg4fp8N5tw1lvlNu1003__mC0)

# Phân tích ca sử dụng Maintain Employee Information
1. Mô tả

Ca sử dụng này cho phép Payroll Administrator duy trì thông tin nhân viên. Điều này bao gồm thêm, thay đổi và xóa thông tin nhân viên khỏi hệ thống.

2. Biểu đồ tuần tự

![Sequence Diagram 'Maintain Employee Information'](https://www.planttext.com/api/plantuml/png/x5NBQi905DtdAowk56m_m4LHL8eBGIgkIXVJv4g79ZFfvAQIR-kYdzHVw9qyZ36fZbAwgc2GEEVSSyyvcg-Fpt52mb0QXPxmIHjOYSpeC9m4aLGo8IFufXVp4UdBM2Y2UHI7EaFSB3flJxKYIu3TAC_h6W0tTmUy8rXRJT1R2gc8t_llOA6ssaI2f5OzhqPOV1Vl25P6Hp41eu3tOnZq9q4mX4qS2C8Xp314me6RAZxhKydZUI8aU6IowiYJ1_owK1HMcmN8cuP9pk4YPgu8st3eAn7nMfJ5V4NoRmSTgjfPsULKqAscVVgGOmHJWsmbADpLU8E-Da43_jFWUrHeBC4Ul9WvpBKUp6GIXo9hZZv2dyfX_Q9tBJ3xK6PRTEHtuYrLNP5ivpvTHZxWMue9rKZ9FnPupjpyj7Wo4j-nIU2K8KDJequ0psVOnhfuLKHqkhTdEf_c55Ts_tZ-1RtdprjfedB-GUsAlwJ_slrzxNBl_2AN_1dZR5uLPc2pgu3dlMl0QWUSV5iAyrhBjyhtmssNndonJ_Ll0000__y30000)

**Giải thích**

PayrollAdministrator (Quản trị viên Lương)
  - Tương tác với giao diện người dùng để thêm, cập nhật, hoặc xóa thông tin nhân viên.
  - Nhập thông tin nhân viên mới, xác nhận việc xóa nhân viên, và thực hiện các chỉnh sửa cần thiết.

EmployeeUI (Lớp giao diện người dùng)
  - Hiển thị các lựa chọn thao tác (Thêm, Cập nhật, Xóa) cho Payroll Administrator.
  -Nhận thông tin nhân viên từ Payroll Administrator để thêm mới hoặc cập nhật.
  - Xác nhận thao tác xóa nhân viên với Payroll Administrator.
  - Hiển thị ID nhân viên mới hoặc thông tin cập nhật cho Payroll Administrator.

EmployeeController (Lớp điều khiển)
  - Xử lý và điều phối yêu cầu thêm, cập nhật, hoặc xóa thông tin nhân viên từ EmployeeUI.
  - Gửi yêu cầu tới lớp Employee để tạo, truy xuất, cập nhật, hoặc đánh dấu nhân viên cần xóa.
  - Truyền thông tin hoặc xác nhận về trạng thái nhân viên đến EmployeeUI.

Employee (Lớp thực thể nhân viên)
  - Tạo và lưu trữ thông tin nhân viên mới, bao gồm việc sinh mã ID độc nhất.
  - Truy xuất thông tin nhân viên để hiển thị cho Payroll Administrator trong quá trình cập nhật hoặc xóa.
  - Cập nhật các chi tiết nhân viên khi cần.
  - Đánh dấu nhân viên cần xóa để hệ thống trả lương cuối cùng trước khi xóa khỏi hệ thống.

3. Biểu đồ lớp

![Class Diagram 'Maintain Employee Information'](https://www.planttext.com/api/plantuml/png/V5DBJWCn3Dtd55x2OYumGbMH2b8bYX250xWJjusKIORO0KM8ax7WI5o1TEX0-jr4odlFVdRiV7z-ZLamI6ojQYmommEcuAszrgrnXYMW-03l2g02BB7ff0RZf2SSjbJ3N89ngmmmMMhaDhf6Z7SNbpMyUgFLXzfQtBITzOdeURfD_1j0UWWfSbNPf8ioGS42rOOxYsb8D7LB_sS3G4ue3Dmcik0QxvOcj9FiUBwu6JfSqT0wRT6xt7uDc_Dg48wo0BKUheLNx3GA7I7qnlsGEAXXp_pCa_-BdbAtI-JQ0Z7lOEmRWtPEJGn6qdri5nHs1DtQEpg2CreCgGRjuy9I3wrz33OzvauBU4LoOZXyWidD7rszgXgL2zE_00LiXE7Do5eLN2aTnbT3e9T8dENOxnQhVKaPblLj3pFasQ4QazFvR_m0003__mC0)

**Các lớp phân tích và nhiệm vụ của từng lớp**

PayrollAdministrator
  - Nhiệm vụ: Đại diện cho người sử dụng chính, người thực hiện các thao tác duy trì thông tin nhân viên.
  - Thuộc tính:
    + administratorID
    + name
  - Phương thức:
    + selectFunction(): Chọn chức năng (thêm, cập nhật, hoặc xóa).

EmployeeManager
  - Nhiệm vụ: Xử lý các thao tác thêm, cập nhật và xóa thông tin nhân viên.
  - Thuộc tính:
    + employeeList
  - Phương thức:
    + addEmployee(): Thêm nhân viên mới.
    + updateEmployee(): Cập nhật thông tin nhân viên.
    + deleteEmployee(): Xóa thông tin nhân viên.

Employee
  - Nhiệm vụ: Đại diện cho thông tin nhân viên trong hệ thống.
  - Thuộc tính:
    + employeeID
    + name
    + employeeType (giờ, lương, hoặc hoa hồng)
    + address
    + socialSecurityNumber
    + phoneNumber
    + salary
    + hourlyRate
  - Phương thức:
    + getEmployeeInfo(): Truy xuất thông tin nhân viên.
    + setEmployeeInfo(): Cập nhật thông tin nhân viên.

EmployeeUI
  - Nhiệm vụ: Giao diện cho Payroll Administrator để nhập và xem thông tin nhân viên.
  - Thuộc tính:
    + selectedFunction
    + inputData
  - Phương thức:
    + displayEmployeeInfo(): Hiển thị thông tin nhân viên.
    + enterEmployeeData(): Yêu cầu người dùng nhập thông tin nhân viên.
    + confirmDeletion(): Xác nhận thao tác xóa.
  
**Quan hệ giữa các lớp**
  - PayrollAdministrator sử dụng EmployeeUI để chọn chức năng (thêm, cập nhật, hoặc xóa).
  - EmployeeUI tương tác với EmployeeManager để thực hiện chức năng đã chọn và yêu cầu thêm thông tin   - từ lớp Employee khi cần.
  - EmployeeManager trực tiếp quản lý dữ liệu trong Employee, thực hiện các thao tác thêm, cập nhật hoặc xóa.

# Phân tích ca sử dụng Run Payroll
1. Mô tả

Ca sử dụng này mô tả cách tính lương vào mỗi thứ Sáu và ngày làm việc cuối cùng của tháng.

2. Biểu đồ tuần tự

![Class Diagram 'Run Payroll'](https://www.planttext.com/api/plantuml/png/V5DBJiCm4Dtx5AEiMWaka0Mge4LaGLM98jQkCsciE7Oq7YzoDXOSYIjWbxYjQCicqRoPz_74-VxyMdYMnA4tGYfs11ivaZFclH8x5smjQSpGaxEStaW2BMiUOTKFnes8kTxg7fMaEjSJCPUFqdPRajP79-si44Slk7-uT2c1WftGsLnSz1Cf9oXXZxmoUgzt1ZFe8ukG0ramsZEu1d0Q0SmpGXZd1cZYqL6gzjWGS9aeEUOp7XnVN20_ovIgdaVMvDYcreUZ3kjRKXDOWf961ICPryWHJ8ALRTpTkSYPj3rCnLeQJY9zt2_qoAshGNiebffGCInnS5vp4GTl1FZpGKeOo2dq_WmxPVbrdH_KfY1ycdjZoS779XgFrqAzIcqAY5ikDbfrzs7u9zVnNgH4sYPVrQBgheL1UtE_fylHI-gU7ItHO0fRDMl46kjuFn9TBE8p_W4_0000__y30000)

**Giải thích**

 - PayrollUI: Khởi tạo quá trình xử lý bảng lương và hiển thị trạng thái hoặc kết quả cho người dùng.
  - PayrollController: Điều phối toàn bộ quy trình chạy bảng lương, lấy danh sách nhân viên, tính toán và thực hiện thanh toán dựa trên phương thức đã chọn.
  - Employee:Đại diện cho từng nhân viên và lưu trữ các thông tin chi tiết như mức lương, phương thức thanh toán và trạng thái xóa.
  - Timecard: Quản lý giờ làm việc của từng nhân viên để cung cấp dữ liệu tính lương.
  - Payroll: Thực hiện các phép tính cho lương ròng và áp dụng các khoản khấu trừ hợp pháp.
  - BankTransaction: Xử lý giao dịch ngân hàng cho các khoản thanh toán qua chuyển khoản.

3. Biểu đồ lớp

![Class Diagram 'Run Payroll'](https://www.planttext.com/api/plantuml/png/X9JDQjmm4CVlUWeTRTYyW2WXf9kGXIO4ajBpr9hiYfKbev42flJ9UkWZzHKgoIlRsRN9PRqQpVpdDn_slpz_RyY3yw7LhD50n9-XTrRhxpl-Yt7kWZaPgZeUEwUCZuRcWCsnmhRRcJSh-5tRQTiZRhZ1T2tulRRWKuHKr6deJo8l7doWYl93y1SVzVOr-yq-9lzgZKzFT4iGU_HtMktLJuqbCLMruDyK-I_5SfrfROD4nHGr4dB-Fp4dnHRSyTwwBMhqofhTsnEYHBdeFR8MKqOidZjPgef60WskD2FnGD-YyO_e3tRkbzAZd048VckjHZ3nKb4fDZgKDZJ1kQYq1H_Pqcyz3zdd8QHKM_IWTExEoJBnlweM6t1odVzWWwCVDi5DHSWnvv3f8JbLb_4RdXThSDrmD78a7QJEXvuv6j1DqD7jATUmj6ANLFL41rsd-otAqAG-qcNyPVfRCCTN1uOWnsGCFvq_T0HQ6uoVJNJOi5duvo_5DAc8CBrjLrVN2-ilk3BAgzWGOfUtAMPSGy4THavyZwwZSL5L9Evt9P7ID86jA8yB8dYWA3gUFnETJMXDkynSb1PEzV5bzLXSS8PEpLpJFH_ch7-SdL-kr35ack_0yDbYZDt4DOwVoly0003__mC0)

**Các lớp phân tích và nhiệm vụ của từng lớp**

PayrollUI
  - Nhiệm vụ: Giao diện người dùng để khởi tạo quá trình chạy bảng lương và hiển thị trạng thái hoặc kết quả.
  - Phương thức:
    + runPayroll(): Gửi yêu cầu chạy bảng lương tới PayrollController.
    + printPaycheck(empInfo: Employee, netPay: Float): In phiếu lương cho nhân viên.
    + displayPayrollStatus(status: String): Hiển thị trạng thái quá trình chạy bảng lương.

PayrollController
  - Nhiệm vụ: Điều phối toàn bộ quá trình chạy bảng lương, bao gồm lấy danh sách nhân viên, tính toán lương, và xử lý thanh toán.
  - Phương thức:
    + runPayroll(): Quản lý toàn bộ quá trình chạy bảng lương.
    + getEligibleEmployees(): List<Employee>: Lấy danh sách nhân viên đủ điều kiện nhận lương.
    + processEmployeePay(employee: Employee): Tính toán và xử lý thanh toán cho từng nhân viên.
    + markForDeletionIfNeeded(employee: Employee): Đánh dấu xóa nhân viên nếu cần.

Employee
  - Nhiệm vụ: Lưu trữ thông tin chi tiết của từng nhân viên và cung cấp các phương thức liên quan đến nhân viên.
  - Thuộc tính:
    + employeeId: String
    + salary: Float
    + paymentMethod: String
    + markedForDeletion: Boolean
  - Phương thức:
    + isEligibleForPayroll(currentDate: Date): Boolean: Kiểm tra điều kiện nhận lương.
    + getPaymentDetails(): Payment: Lấy thông tin thanh toán của nhân viên.

Timecard
  - Nhiệm vụ: Quản lý và cung cấp dữ liệu về giờ làm việc của nhân viên.
  - Thuộc tính:
    + employeeId: String
    + hoursWorked: Float
    + date: Date
  - Phương thức:
    + getHours(employeeId: String): Float: Lấy số giờ làm việc của nhân viên.

Payroll
  - Nhiệm vụ: Thực hiện các phép tính chi tiết cho quá trình chạy bảng lương.
  - Phương thức:
    + calculateNetPay(empInfo: Employee, hoursWorked: Float): Float: Tính lương ròng.
    + applyDeductions(empInfo: Employee): Float: Áp dụng các khoản khấu trừ hợp pháp.

BankTransaction 
  - Nhiệm vụ: Xử lý giao dịch ngân hàng cho các khoản thanh toán qua chuyển khoản.
  - Thuộc tính:
    + transactionId: String
    + amount: Float
  - Phương thức:
    + processTransaction(empInfo: Employee, netPay: Float): Boolean: Thực hiện giao dịch ngân hàng.

**Quan hệ giữa các lớp**
  - PayrollUI giao tiếp với PayrollController để khởi tạo quá trình chạy bảng lương và nhận trạng thái từ quá trình.
  - PayrollController tương tác với Employee để lấy danh sách nhân viên đủ điều kiện nhận lương.
  - PayrollController sử dụng Timecard để lấy dữ liệu giờ làm việc của từng nhân viên.
  - PayrollController gọi Payroll để tính toán lương ròng cho từng nhân viên.
  - PayrollController tương tác với BankTransaction nếu phương thức thanh toán của nhân viên là chuyển khoản trực tiếp.
  - PayrollController tương tác lại với Employee để đánh dấu xóa nhân viên nếu cần thiết sau khi xử lý lương.

# Code java mô phỏng ca sử dụng Maintain Timecard.

import java.util.ArrayList;
import java.util.Date;
import java.util.Scanner;

class Employee {
    private String employeeId;
    private String name;

    public Employee(String employeeId, String name) {
        this.employeeId = employeeId;
        this.name = name;
    }

    public String getEmployeeId() {
        return employeeId;
    }

    public String getName() {
        return name;
    }
}

class Timecard {
    private String employeeId;
    private Date date;
    private float hoursWorked;

    public Timecard(String employeeId, Date date, float hoursWorked) {
        this.employeeId = employeeId;
        this.date = date;
        this.hoursWorked = hoursWorked;
    }

    public String getEmployeeId() {
        return employeeId;
    }

    public Date getDate() {
        return date;
    }

    public float getHoursWorked() {
        return hoursWorked;
    }

    @Override
    public String toString() {
        return "Timecard{" +
                "employeeId='" + employeeId + '\'' +
                ", date=" + date +
                ", hoursWorked=" + hoursWorked +
                '}';
    }
}

class TimecardController {
    private ArrayList<Timecard> timecards = new ArrayList<>();

    public void addTimecard(String employeeId, Date date, float hoursWorked) {
        Timecard timecard = new Timecard(employeeId, date, hoursWorked);
        timecards.add(timecard);
        System.out.println("Timecard đã được ghi nhận: " + timecard);
    }
    
    public void viewTimecards(String employeeId) {
        System.out.println("Danh sách thẻ chấm công của nhân viên ID: " + employeeId);
        for (Timecard tc : timecards) {
            if (tc.getEmployeeId().equals(employeeId)) {
                System.out.println(tc);
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        TimecardController timecardController = new TimecardController();

        Employee employee1 = new Employee("E001", "John Doe");
        Employee employee2 = new Employee("E002", "Jane Smith");

        System.out.println("Nhập số giờ làm việc của nhân viên " + employee1.getName() + ":");
        float hoursWorked1 = scanner.nextFloat();
        timecardController.addTimecard(employee1.getEmployeeId(), new Date(), hoursWorked1);

        System.out.println("Nhập số giờ làm việc của nhân viên " + employee2.getName() + ":");
        float hoursWorked2 = scanner.nextFloat();
        timecardController.addTimecard(employee2.getEmployeeId(), new Date(), hoursWorked2);

        System.out.println("\nDanh sách thẻ chấm công của " + employee1.getName() + ":");
        timecardController.viewTimecards(employee1.getEmployeeId());

        System.out.println("\nDanh sách thẻ chấm công của " + employee2.getName() + ":");
        timecardController.viewTimecards(employee2.getEmployeeId());

        scanner.close();
    }
}
