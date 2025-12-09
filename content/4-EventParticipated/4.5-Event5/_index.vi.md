---
title: "Sự kiện 5"
date: "2025-10-22T03:10:22Z"
weight: 1
chapter: false
pre: " <b> 4.5. </b> "
---

# Báo cáo tổng kết: AWS Cloud Mastery Series #3 – AWS Well-Architected Security Pillar

## Mục tiêu sự kiện
- Cung cấp cái nhìn toàn diện về nguyên tắc cốt lõi của AWS Security và kiến trúc Identity hiện đại.
- Làm rõ vai trò, khác biệt và các use case thực tế giữa IAM và IAM Identity Center.
- Minh họa cách Single Sign-On (SSO) cải thiện hiệu quả vận hành và kiểm soát truy cập tập trung.
- Giải thích và áp dụng các cơ chế bảo mật nâng cao: SCPs, permission boundaries, MFA, IAM Access Analyzer.
- Hướng dẫn thực hành chu trình vòng đời danh tính (identity lifecycle) qua demo onboarding và cấu hình SSO.

## Diễn giả
- Văn Hoàng Kha – AWS Community Builder
- Cloud Club Captains đến từ HCMUTE, HUFLIT & PTIT
- Đinh Lê Hoàng Anh – Cloud Engineer Trainee, First Cloud AI Journey
- Huỳnh Hoàng Long – Cloud Engineer Trainee, First Cloud AI Journey

## Các điểm nhấn chính (Key Highlights)
- Phân tích rõ ràng sự khác nhau giữa IAM và IAM Identity Center, thời điểm và bối cảnh sử dụng phù hợp cho từng dịch vụ.
- Giải thích lợi ích của SSO và xác thực tập trung, nâng cao bảo mật và khả năng quản trị (governance) đa tài khoản.
- Đi sâu vào SCPs và permission boundaries: thiết lập guardrails và cơ chế phân quyền ủy quyền (delegated control) ở môi trường multi‑account.
- Hướng dẫn thiết lập IAM Access Analyzer, kích hoạt MFA và xoay vòng thông tin xác thực (credential rotation) an toàn.
- Live demo: Onboarding người dùng mới vào IAM Identity Center và cấu hình SSO qua AWS CLI.
- Bức tranh tổng thể về AWS security lifecycle: identity, detection, infrastructure protection, data security, incident response, application security.

## Bài học chính (Key Takeaways)
- Identity là nền tảng của AWS Security; IAM Identity Center đơn giản hóa quản lý truy cập ở quy mô lớn.
- SCPs và permission boundaries có mục tiêu khác nhau nhưng phối hợp để thực thi quản trị chặt chẽ trên nhiều tài khoản.
- MFA, phân tích truy cập liên tục và “vệ sinh” thông tin xác thực là thiết yếu để ngăn truy cập trái phép.
- GuardDuty, CloudTrail, Security Hub đóng vai trò quan trọng cho giám sát thời gian thực và hiển thị mối đe dọa.
- Kiến trúc bảo mật hiệu quả đòi hỏi phòng thủ nhiều lớp, mã hóa toàn diện và quy trình tự động khắc phục (automated remediation).
- Chuyển giao ứng dụng an toàn cần kiểm soát CI/CD chặt chẽ, quản lý secrets và bảo vệ ở thời gian chạy (runtime protections).

## Trải nghiệm sự kiện
Buổi chia sẻ cung cấp hướng dẫn đầy đủ từ nguyên lý đến cấu hình thực hành. Phần tổng quan security lifecycle giúp kết nối các mảnh ghép: identity, detection, hạ tầng, dữ liệu và ứng phó sự cố thành một bức tranh mạch lạc thay vì các công cụ rời rạc. Live demo cuối giờ cho thấy luồng công việc thực tế, nối liền lý thuyết, kiến trúc và các bước triển khai – đặc biệt hữu ích cho bối cảnh multi‑account và kiến trúc identity quy mô lớn.
## Thư viện ảnh
<img src="/images/4-EventParticipated/IMG_20251129_090105.jpg" width="500" alt="Event Photo 1">
