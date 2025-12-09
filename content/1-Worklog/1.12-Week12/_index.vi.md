---
title: "Nhật ký công việc Tuần 12"
date: "2025-10-22T03:10:22Z"
weight: 2
chapter: false
pre: " <b> 1.12. </b> "
---

### Mục tiêu Tuần 12:

* Hoàn thiện tính năng cuối: đồng bộ dữ liệu người dùng (DynamoDB) vào datasets Personalize (Items, Interactions).
* Hợp nhất mã nguồn (merge), giải quyết xung đột (resolve conflicts), kiểm thử toàn bộ Personalize (realtime + batch) và hoàn tất tài liệu/triển khai.

### Các nhiệm vụ cần thực hiện trong tuần này:
| Ngày | Nhiệm vụ                                                                                                                                                                                                                           | Ngày       | Ngày hoàn thành | Tài liệu tham khảo                                                                               |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------------------------------------------------------------------------------------ |
| 2   | - Thiết kế luồng ETL đồng bộ: DynamoDB (Users/Ratings) → S3 (CSV/JSON) → Personalize Datasets (Items, Interactions) <br> - Chuẩn hóa schema và mapping field (userId, itemId, timestamp, eventType)                                | 11/24/2025 | 11/24/2025      | https://docs.aws.amazon.com/personalize/latest/dg/datasets-and-schemas.html                     |
| 3   | - Viết Lambda ETL: scan DynamoDB theo trang (pagination), chuyển đổi dữ liệu và ghi ra S3 theo partition/date <br> - Thêm kiểm soát idempotent, loại trùng, và xác thực dữ liệu                                                     | 11/25/2025 | 11/25/2025      | https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/dynamodb-example-table-read.html |
| 4   | -  Demo Import/Update datasets Personalize: Items + Interactions <br> - Chạy re-train/re-deploy solution khi dữ liệu đổi đáng kể (demo thủ công)                                                                                      | 11/26/2025 | 11/26/2025      | https://docs.aws.amazon.com/personalize/latest/dg/recording-events.html                         |
| 5   | - Hợp nhất mã nguồn (merge vào branch main): giải quyết xung đột ở SAM templates, Lambda handlers (realtime/batch/etl) <br> - Thiết lập CI kiểm thử lint/build/deploy trên PR                                                     | 11/27/2025 | 11/27/2025      | https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html |
| 6   | - Kiểm thử end-to-end: <br> Realtime (PutEvents/PutItems → GetRecommendations) <br> Batch (ETL → Batch Inference → Cache DynamoDB → Fallback) <br> - Rà soát chi phí/hiệu năng, hoàn thiện tài liệu và checklist bàn giao         | 11/28/2025 | 11/28/2025      | https://aws.amazon.com/personalize/pricing/                                                     |

### Thành tựu Tuần 12:

**Mục tiêu 1**: Đồng bộ dữ liệu người dùng vào Personalize  
✅ Hoàn thiện pipeline ETL từ DynamoDB sang S3 với phân vùng theo ngày, chuẩn hóa schema Items/Interactions.  
✅ Tự động import/update datasets Personalize và kích hoạt re-train/re-deploy khi có thay đổi dữ liệu lớn.

**Mục tiêu 2**: Hợp nhất mã nguồn & xử lý xung đột  
✅ Merge các nhánh tính năng vào main; giải quyết xung đột ở CloudFormation/SAM và Lambda.  


**Mục tiêu 3**: Kiểm thử toàn diện Personalize (hybrid)  
✅ Kiểm thử realtime: PutEvents/PutItems, xác minh GetRecommendations theo người dùng.  
✅ Kiểm thử batch: chạy batch-inference, nạp cache DynamoDB, và kiểm tra fallback khi campaign bị throttled/offline.  
✅ Ghi nhận metric: độ trễ, tỉ lệ lỗi.

**Kết quả chính**:
+ Dữ liệu đồng bộ demo: Items/Interactions được cập nhật từ DynamoDB theo lịch, đảm bảo độ tươi cho gợi ý.  
+ Kiến trúc lai ổn định: Realtime cung cấp gợi ý tức thì; batch đảm bảo phủ rộng và độ trễ thấp qua cache.  
+ Vận hành & chi phí: Tối ưu ETL/Lambda, giảm tính toán dư thừa; tài liệu hóa quy trình và checklist bàn giao hoàn chỉnh.