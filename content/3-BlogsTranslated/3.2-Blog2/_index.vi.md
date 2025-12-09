---
title: "Blog 2"
date: "2025-10-22T03:10:22Z"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

**Bài dịch tiếng Việt đầy đủ:** [Cách sử dụng Capacity Blocks cho học máy với AWS Batch](https://docs.google.com/document/d/1D7AVfxZyAT4jN8zFCI4hJOG-mrDI1M_hToxgOzwP7Rg/edit?usp=sharing)  
**Bài gốc:** [How to use Capacity Blocks for ML with AWS Batch](https://aws.amazon.com/vi/blogs/hpc/how-to-use-capacity-blocks-for-ml-with-aws-batch/)

# Tóm tắt: Capacity Blocks cho ML với AWS Batch

## Khái niệm chính
- Capacity Blocks for ML (CBML): Đặt trước (reservation) các GPU “hot” như NVIDIA H100 cho một khung thời gian cụ thể trong tương lai.
- AWS Batch: Dịch vụ xếp hàng và lập lịch job, tự động kích hoạt công suất đã đặt đúng cửa sổ reservation.

---

## Cách triển khai
1) Mua Capacity Block  
- Chọn loại GPU, số lượng, thời lượng và thời điểm sử dụng trong tương lai.

2) Tạo EC2 Launch Template  
- InstanceMarketOptions.MarketType = "capacity-block"  
- Thêm CapacityReservationId của reservation  
- Khai báo AMI, Security Groups, cấu hình mạng (có thể EFA), v.v.

3) Cấu hình AWS Batch  
- Tạo Compute Environment (CE) trỏ về Launch Template trên, bảo đảm đúng AZ/instance type với reservation.  
- Chọn allocation strategy: BEST_FIT.  
- Tạo Job Queue gắn với CE.

4) Gửi Job (Submit)  
- Có thể đẩy job trước. Batch sẽ “đợi” đến khi cửa sổ reservation mở để khởi chạy instance và chạy job.

---

## Lưu ý quan trọng
- Môi trường dùng một lần: CE cho CBML nên coi là “dùng và bỏ”. Khi reservation hết hạn, hãy xóa CE đó.
- Logic scale:
  - minvCpus = 0: Batch đợi đến cửa sổ reservation mới scale lên.  
  - minvCpus > 0: Vẫn đợi cửa sổ nhưng có thể chuẩn bị trước một số tài nguyên.  
  - Multi-node (MNP): Đặt maxvCpus bằng đúng tổng công suất đặt trước để bảo đảm các node khởi chạy đồng thời.
- Tương thích: AZ và instance type của CE phải khớp với reservation; sai là không khởi chạy được.

---

## Lựa chọn thay thế
- On-Demand Capacity Reservations (ODCR): Phù hợp workload quan trọng (không GPU), linh hoạt và có thể gom nhóm.  
- Spot Instances: Cho single-node job chấp nhận gián đoạn; P5 Spot có thể tiết kiệm chi phí lớn (tới ~75%).

---

## Kết luận
Kết hợp AWS Batch với Capacity Blocks giúp tự động hóa hạ tầng cho huấn luyện ML hiệu năng cao: bạn nhận đúng “công suất GPU đã trả tiền” vào đúng thời điểm, giảm rủi ro thiếu tài nguyên và tối ưu chi phí vận hành.