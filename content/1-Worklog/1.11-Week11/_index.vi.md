---
title: "Nhật ký công việc Tuần 11"
date: "2025-10-22T03:10:22Z"
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu Tuần 11:

* Thiết kế và triển khai kiến trúc gợi ý lai (Thời gian thực + Batch-inference) cho Rafilm.
* Ổn định thu thập sự kiện (putEvents/putItems) và pipeline batch ban đêm bằng SAM.

### Các nhiệm vụ cần thực hiện trong tuần này:
| Ngày | Nhiệm vụ                                                                                                                                                                                                                  | Ngày       | Ngày hoàn thành | Tài liệu tham khảo                                                                                 |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | --------------------------------------------------------------------------------------------------- |
| 2   | - Củng cố kiến trúc: xác định luồng dữ liệu giữa API Gateway → Lambda → Personalize (Realtime) và S3 → Personalize Batch → DynamoDB (Cache) <br> - Tài liệu hóa ranh giới thành phần và chiến lược xử lý lỗi              | 11/17/2025 | 11/17/2025      | https://docs.aws.amazon.com/personalize/latest/dg/recording-events.html                            |
| 3   | - Triển khai theo dõi sự kiện realtime: tích hợp `PutEvents` và `PutItems` vào Lambda sau API Gateway <br> - Thêm xác thực request, cơ chế retry và logging có cấu trúc                                                   | 11/18/2025 | 11/18/2025      | https://docs.aws.amazon.com/personalize/latest/dg/API_UBS_PutEvents.html                           |
| 4   | - Nâng cấp pipeline batch: lên lịch batch-inference (EventBridge) → Personalize → ghi output ra S3 → chuyển đổi sang cache DynamoDB <br> - Thêm loại trùng (de-dup) và ghi idempotent                                      | 11/19/2025 | 11/19/2025      | https://docs.aws.amazon.com/personalize/latest/dg/batch-inference.html                             |
| 5   | - Tối ưu Lambda: tách handler (realtime vs batch ETL), giảm cold start, thêm kiểm soát concurrency và backoff <br> - Thêm feature flags để chuyển đổi giữa phản hồi realtime và cache                                     | 11/20/2025 | 11/20/2025      |      |
| 6   | - Kiểm thử end-to-end: mô phỏng traffic người dùng, xác minh độ tươi mới và cơ chế fallback <br> - Rà soát chi phí/hiệu năng và hoàn tất tài liệu hóa                                                                      | 11/21/2025 | 11/21/2025      | https://aws.amazon.com/personalize/pricing/                                                         |

### Thành tựu Tuần 11:

**Mục tiêu 1**: Thiết kế Kiến trúc Hybrid (Realtime + Batch)  
✅ Hoàn tất luồng gợi ý hai nhánh:
- Nhánh thời gian thực: API Gateway → Lambda (PutEvents/PutItems) → Personalize Campaign (GetRecommendations).
- Nhánh batch: Lịch EventBridge ban đêm → Personalize Batch Inference → S3 output → Lambda ETL → DynamoDB cache.

**Mục tiêu 2**: Thu thập & Cache bền vững  
✅ Triển khai xác thực sự kiện, logging có cấu trúc và retry cho ingestion thời gian thực.  
✅ Xây dựng ETL batch idempotent với loại trùng để giữ cache DynamoDB nhất quán và tránh ghi thừa.

**Mục tiêu 3**: Vận hành OK  
✅ Tách handler Lambda để rõ ràng và mở rộng; tinh chỉnh bộ nhớ/timeout.  
✅ Thêm feature flags để định tuyến request: ưu tiên realtime; fallback sang DynamoDB cache khi campaign bị throttle hoặc offline.

**Kết quả chính**:
+ Realtime vs Batch: Realtime cung cấp gợi ý cập nhật tức thời; batch đảm bảo phủ rộng và chi phí thấp qua cache.  
+ Khả năng chịu lỗi: Logic fallback bảo đảm dịch vụ liên tục bằng kết quả cache khi realtime suy giảm.    
+ Quan sát: Nhật ký/metric tập trung (thời lượng, lỗi, tỷ lệ cache hit) hỗ trợ tối ưu hiệu năng và ứng phó sự cố.