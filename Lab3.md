# Lab3. Identify design elements

## 1. Subsystem context diagrams
1.1 Subsystem Context Diagrams
1.1.1 BankSystem Subsystem

![BankSystem Subsystem Diagram](https://www.planttext.com/api/plantuml/png/h5F1JiCm3BtdAtnZI5IxJzKqDe6q2q9mu6nIZqPDayf96HNmPHpu97w1PEb6kmbneQeKzptx-TbLlZu-5yuZ-xRMmbNADCXOWzJe7BmA2CyIPVN4jZN5ochBy50gJucnN10dTAb3sWwzPBRRO_3Q6d-3DGLMeHRlGfp1BNPijLu5Afx4VTkjyYKuJqpMTms9X9vcvxbC7_DvRtKw1MuDD2brSfxwh9TeglikADQWJD3Te2HnY4PydX_mWsf1ZNNAJp1Oa2N92cQm3o-Yeeq20Op7scmir-YLDNtxWNgQ1CCBhdrq2MpOldJza2CdHod_vUVAUEKLkP-z9f4yfyY4FWCpW_9OUqTw5xjIDKwS_f8icu_MEOD2CKc_z-nWryl1iq8nsljRbWsc7t5HTE_oX3Ws-LlT7sLYGQQ8T-0R003__mC0)

- IBankSystem: nhằm giao tiếp với các BankSystem bên ngoài.
  + deposit(): gửi tiền lương chỉ định (aPaycheck) vào ngân hàng được chỉ định (intoBank).

1.1.2 PrintService Subsystem

![PrintService Subsystem Diagram](https://www.planttext.com/api/plantuml/png/d591JiCm4Bpx5QjUA1AqSAsYgBG2gHTKqGCNBYRP4YkERQqTIWIyZ0DFuWlOSHf8Uq54aUoT6S-iD_dw-9nRnydLbMIs5CfmuXLaabiBhmpyi-1P-KIwLlbIIqrmNmY7aT6K8qLq8RsiHQ-8zEuGlD7AtV8AFIkuPE-CdS2QDwIbN7egh4XTx4wu0gn3GkqQWooYn-eaoMAHfbshqobGhS14wVWqvgmMN9MRnZjM89JttV8CMR-3rPfyiK5w5hvAafxfVKqGZBbl8IimAs46--rPSDGXm8DXMQcjfeexeLKN_oizteJx5spzQ2DeIByq-qiEEpaGzVtaQBGL_-xeMZdX1DgVoKQJ9C70-9oWkaFP7hA5C9ODXtH-dlR7s9-PjtGuQtRyJKSNaydbg7KP9ivWP3hR5aTwKAsMiJcgFFo-tm000F__0m00)

- IPrintService: nhằm giao tiếp với tất cả máy in.
  + print(): in phiếu lương đã cho (aPaycheck) trên máy in được chỉ định (onPrinter).


1.1.3 ProjectManagementDatabase Subsystem

![PrintService Subsystem Diagram](https://www.planttext.com/api/plantuml/png/f9F1Ji9048Rl-nIJNWGJYbu9QH2C2OaI8oPUl0pRiLrfTvlPhKhK9_FW8_aABYm1GUp5feVs_-VlVFdRVdry3gn3TdLP23jNkaB64cI1riAh07yCKSupDhLEHwOm37UvSXGSmobnK8U57rkfPypcUL-yCDfDi2JlAYp4kn17SAjAaiZ-iTgnAGhYi5U4xGViVb-6coHPmtMxa943MJEJTk3McLPxnyrHPsH1cfIsJbsbwEX0nEBJZho27GzHpwSBwwW4fHtn0qeIcoiONxDv9EckK6D6fOSvHuSpjEIfDsCRReyrof4pcjJbZDYs9FjMVJVGWwbZfRDsRyaT9YwLTG7Z1qLe2Vq9jfxP85PiNXRh0fk8zXB_v0hxHZkoXxsX0fqoskQgik9ld3X-IneAR4mcUsiRtiFluGEVM7GInySHT3fDH3s8ucqBKrEpf7ljawUH40FIwV9l-WO00F__0m00)

- IProjectManagementDatabase: nhằm giao tiếp với Cơ sở dữ liệu quản lý dự án cũ (Project Management Database) có chứa thông tin về số chi phí dự án.
  + getChargeNumbers(): lấy lại số phí có sẵn.

## 2. Analysis class to design element map

| Analysis Class | Design Element |
|---|---|
| LoginForm | LoginForm |
| MaintainTimecardForm | MainEmployeeForm<br>TimecardForm |
||MainApplicationForm|
| TimecardController | TimecardController |
| SystemClockInterface | SystemClockInterface |
| PayrollController | PayrollController |
| Paycheck | Paycheck |
| HourlyEmployee | HourlyEmployee |
| Timecard | Timecard |
| PurchaseOrder | Purchase Order |
| CommissionedEmployee | CommissionedEmployee |
| SalariedEmployee | SalariedEmployee |
| Employee | Employee |
| BankSystem | Banksystem subsystem |
|| IBankSystem interface |
| PrinterInterface | PrintService subsystem |
|| IPrintService interface |
| ProjectManagementDatabase | ProjectManagementDatabase subsystem |
|| IProjectManagementDatabase interface |

## 3. Design element to owning package map

| Design Element | "Owning" Package |
|---|---|
| LoginForm | Middleware: Security: GUI Framework |
| MainEmployeeForm<br>TimecardForm | Applications: Employee Activities |
| MainApplicationForm | Middleware: Security: GUI Framework |
| TimecardController | Applications: Employee Activities |
| SystemClockInterface | Applications: Payroll |
| PayrollController | Applications: Payroll |
| Paycheck | Business Services: Payroll Artifacts |
| HourlyEmployee | Business Services: Payroll Artifacts |
| Timecard | Business Services: Payroll Artifacts |
| PurchaseOrder | Business Services: Payroll Artifacts |
| CommissionedEmployee | Business Services: Payroll Artifacts |
| SalariedEmployee | Business Services: Payroll Artifacts |
| Employee | Business Services: Payroll Artifacts |
| BankSystem subsystem | Business Services |
| IBankSystem interface | Business Services: External System Interfaces |
| PrintService subsystem | Business Services |
| IPrintService interface | Business Services: External System Interfaces |
| ProjectManagementDatabase subsystem | Business Services |
| IProjectManagementDatabase interface | Business Services: External System Interfaces |

## 4. Architectural layers and their dependencies

![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bT1Od9sOdggWf9ZGK5EPd9YIMP-dfA2ZKrEOcLgaPsTGZLNBHT2aLDfSMPUQd6nGd1gKLbcScenRgM-cIafEQdbYKMfU8nBB4vL24ejBSPKW-GS1JqzEsnMSs5p3aWjmcekBeVKl1IWFm40003__mC0)

- Application: chứa các phần tử thiết kế ứng dụng cụ thể.
- Business Services: chứa các thành phần nghiệp vụ cụ thể.
- Middleware: cung cấp các tiện ích và dịch vụ độc lập.
