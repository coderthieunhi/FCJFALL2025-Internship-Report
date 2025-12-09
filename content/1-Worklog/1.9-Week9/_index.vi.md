---
title: "Nhật ký công việc Tuần 9"
date: "2025-10-22T03:10:22Z"
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---



### Mục tiêu Tuần 9:

* Tích hợp Amazon Personalize vào dự án Rafilm


### Các nhiệm vụ cần thực hiện trong tuần này:
| Ngày | Nhiệm vụ                                                                                                                                                                                                | Ngày | Ngày hoàn thành | Tài liệu tham khảo                        |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| 2   | - **Chuẩn bị bộ dữ liệu**: <br> Nghiên cứu bộ dữ liệu (chọn MovieLens) <br> - Định dạng dữ liệu theo yêu cầu của Personalize                                                                            | 11/03/2025 | 11/03/2025      | https://grouplens.org/datasets/movielens/ |
| 3   | - **Khởi chạy campaign demo**: <br> + Xác định schema, tạo solution                                                                                              | 11/04/2025 | 11/04/2025      | https://docs.aws.amazon.com/personalize/latest/dg/API_Campaign.html |
| 4   | - **Viết Lambda Function**: <br> Hàm xử lý kết quả từ chiến dịch Amazon Personalize                                                                                  | 11/05/2025 | 11/05/2025      | https://github.com/aws-samples/amazon-personalize-samples <br> |
| 5   | - Nghiên cứu tối ưu chi phí cho Amazon Personalize                                                                                                                  | 11/06/2025 | 11/06/2025      | https://aws.amazon.com/personalize/pricing/ |
| 6   | - **Viết Lambda Function**: <br> Hàm xử lý và kích hoạt batch-inference                                                                                            | 11/07/2025 | 11/07/2025      | 

### Thành tựu Tuần 9:


**Kết quả chính**:

+ Thu thập & Chuẩn bị Dữ liệu: Nghiên cứu và chọn bộ dữ liệu MovieLens cho hệ thống gợi ý, sau đó định dạng và cấu trúc để đáp ứng yêu cầu schema của Amazon Personalize (Users, Items, Interactions).

+ Triển khai Campaign Personalize: Thực hành với Amazon Personalize bằng cách định nghĩa schema, tạo phiên bản solution và khởi chạy chiến dịch demo trực tiếp, thiết lập mô hình gợi ý hoạt động.

+ Phát triển Tích hợp Lambda: Xây dựng và kiểm thử các hàm AWS Lambda để tương tác với chiến dịch Personalize, cho phép backend lấy gợi ý thời gian thực dựa trên đầu vào người dùng.

+ Lập Kế hoạch Kiến trúc Tối ưu Chi phí: Nghiên cứu giá và chiến lược tối ưu của Amazon Personalize, đảm bảo dự án tiết kiệm chi phí khi mở rộng—bao gồm chi phí huấn luyện, suy luận và gợi ý thời gian thực.

+ Khởi tạo Pipeline Batch Inference: Bắt đầu phát triển các hàm Lambda để kích hoạt và xử lý job batch inference, hướng tới cập nhật gợi ý theo lịch trình, quy mô cho toàn bộ người dùng.