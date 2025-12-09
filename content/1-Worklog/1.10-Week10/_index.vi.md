---
title: "Nhật ký công việc Tuần 10"
date: "2025-10-22T03:10:22Z"
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---



### Mục tiêu Tuần 10:

* Tích hợp Amazon Personalize vào dự án Rafilm


### Các nhiệm vụ cần thực hiện trong tuần này:
| Ngày | Nhiệm vụ                                                                                                                                                                                                | Ngày | Ngày hoàn thành | Tài liệu tham khảo                        |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| 2   | - **Triển khai batch-inference**: <br> tạo tài nguyên cần thiết trong SAM: <br> + Bảng cache Dynamo, S3 <br> - **Tối ưu hàm Lambda để kích hoạt batch-inference**                                      | 11/10/2025 | 11/10/2025      | https://docs.aws.amazon.com/personalize/ |
| 3   | - **Gỡ lỗi (Debug)**: <br> + Sửa lỗi batch-job thất bại do sai đường dẫn trong CloudFormation template <br> + Sửa lỗi tạo batch-job dư thừa <br> + Sửa lỗi lệch user-id trong bảng DynamoDB output     | 11/11/2025 | 11/11/2025      | https://docs.aws.amazon.com/personalize/ |
| 4   | - **Nghiên cứu tính năng chiến dịch thời gian thực**: tập trung vào putevents và putitems                                                                          | 11/12/2025 | 11/12/2025      | https://github.com/aws-samples/amazon-personalize-samples <br> |
| 5   | - Triển khai putitems và putevents vào Lambda để theo dõi sự kiện                                                                                                   | 11/13/2025 | 11/13/2025      | https://aws.amazon.com/personalize/pricing/ |
| 6   | - Refactor để mã nguồn gọn hơn, ghi chú comment chi tiết <br>                                                                                                                                | 11/14/2025 | 11/14/2025      | 

### Thành tựu Tuần 10:


**Kết quả chính**:


+ Pipeline Batch sẵn sàng: Đã triển khai hệ thống gợi ý batch tự động, ổn định bằng SAM, Lambda, S3 và DynamoDB.

+ Khắc phục thành công các vấn đề tích hợp giữa CloudFormation, Personalize và tầng dữ liệu.

+ Mở rộng khả năng thời gian thực: Tăng cường bộ máy gợi ý với theo dõi sự kiện trực tiếp, cho phép gợi ý phản hồi nhanh và cá nhân hóa hơn.

+ Cải thiện chất lượng mã: Áp dụng nguyên tắc clean code thông qua refactor, giúp mã dễ mở rộng và bảo trì.

+ Nhận thức Chi phí & Hiệu năng: Tối ưu thực thi Lambda và loại bỏ job dư thừa để tăng hiệu quả và kiểm soát chi phí.