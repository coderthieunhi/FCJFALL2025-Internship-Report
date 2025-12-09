---
title: "Blog 3"
date: "2025-10-22T03:10:22Z"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
**Bài dịch đầy đủ:** [Các phương pháp tốt nhất để tận dụng AWS Systems Manager với AWS Fault Injection Service](https://docs.google.com/document/d/1VPZj-1wk8V3aKY13bVzHVr4j5fdVZIgYAgrMk78rux8/edit?usp=sharing)  
**Bài gốc:** [Best practices for utilizing AWS Systems Manager with AWS Fault Injection Service](https://aws.amazon.com/vi/blogs/mt/best-practices-for-utilizing-aws-systems-manager-with-aws-fault-injection-service/)

# Tóm tắt: Best practices cho AWS Systems Manager (SSM) với AWS Fault Injection Service (FIS)

Bài viết hướng dẫn cách kết hợp AWS Systems Manager (SSM) với AWS Fault Injection Service (FIS) để thực hiện chaos engineering an toàn, linh hoạt và sát thực tế cho nhiều loại ứng dụng (từ custom stack đến SAP).

## Vì sao tích hợp SSM với FIS?
- Mở rộng khả năng: Dùng action `aws:ssm:send-command` để chạy Bash/PowerShell trên target, giúp mô phỏng sự cố phức tạp, tùy biến vượt quá các built‑in actions của FIS.
- Điều khiển tập trung: Quản lý và inject fault vào các managed node (EC2, on‑prem, edge) trên nhiều account/region từ một thí nghiệm duy nhất.

## Best practices cho SSM Documents
- Cấu trúc mô‑đun: Tách thành các bước rõ ràng: validate prerequisites → inject fault → clean up; dễ troubleshoot và rollback.
- Tham số rõ ràng: Khai báo parameter type, description, validation pattern/range (ví dụ: tên ứng dụng/service) để giảm lỗi sử dụng.
- Biến môi trường: Tránh hardcode region/ID; dùng biến sẵn có (ví dụ `AWS_SSM_REGION_NAME`) để tăng portability.
- Phát hiện HĐH: Tự nhận diện OS (Amazon Linux/Ubuntu/Windows) và nhánh lệnh/packager phù hợp để 1 document dùng cho nhiều fleet.
- Preconditions: Điều kiện trước khi chạy step (kiểm tra dependency, chọn Bash hay PowerShell theo platform, v.v.).
- Xử lý lỗi: Dùng `OnFailure: exit` để dừng thí nghiệm ngay khi step fail, báo lỗi về FIS, tránh trạng thái không xác định.
- Idempotency: Kiểm tra state rồi mới hành động (ví dụ chỉ stop service khi đang running) để hỗ trợ retry/resume an toàn.
- Timeouts: Đặt `timeoutSeconds` cho từng step; nếu script treo, hệ thống hủy và kích hoạt clean‑up khôi phục môi trường.
- Logging: Ghi log chi tiết (echo/Write‑Output) và gửi execution logs lên CloudWatch Logs hoặc S3 để phân tích, audit.

## Quy trình thí nghiệm điển hình
1) Validate: Xác nhận platform, agent/package, và permission.  
2) Inject fault: Gây lỗi có kiểm soát (CPU/memory pressure, stop service, latency, packet loss).  
3) Observe: Kiểm tra detection/alert (CloudWatch, runbook).  
4) Clean up: Hoàn nguyên thay đổi, khởi động lại service, xác nhận trạng thái healthy.

## Điểm rút ra
- Kết hợp SSM + FIS nâng độ chân thực của thí nghiệm nhưng vẫn an toàn nhờ parameters, preconditions, và kiểm soát fail/timeout chặt chẽ.
- Tính tái sử dụng/di động đến từ document mô‑đun, script nhận diện OS, và cấu hình dựa trên môi trường.
- Quan sát/ghi log mạnh là thiết yếu để xác thực resilience và rút kinh nghiệm.
- Bước idempotent, giới hạn thời gian giúp tránh drift và đơn giản hóa rollback trong chaos tests.