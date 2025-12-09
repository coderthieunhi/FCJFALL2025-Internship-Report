---
title: "Blog 2"
date: "2025-10-22T03:10:22Z"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---
**FULL VIETNAMESE TRANSLATED BLOG:** [Cách sử dụng Capacity Blocks cho học máy với AWS Batch](https://docs.google.com/document/d/1D7AVfxZyAT4jN8zFCI4hJOG-mrDI1M_hToxgOzwP7Rg/edit?usp=sharing)  
**ORIGINAL BLOG:** [How to use Capacity Blocks for ML with AWS Batch](https://aws.amazon.com/vi/blogs/hpc/how-to-use-capacity-blocks-for-ml-with-aws-batch/)

# Summary: How to use Capacity Blocks for ML with AWS Batch

## Key Concepts
- Capacity Blocks for ML (CBML): Reserve high‑demand GPU instances (e.g., NVIDIA H100) for a specific future window.
- AWS Batch: Schedules/queues jobs and starts instances exactly within your reservation window.

## Implementation Steps
1) Purchase a Capacity Block
- Choose instance type, quantity, AZ, and duration for a future date/time.

2) Create an EC2 Launch Template
- InstanceMarketOptions.MarketType = "capacity-block"
- Include CapacityReservationId
- Define AMI, security groups, subnet/AZ, and optional EFA/networking settings

3) Configure AWS Batch
- Compute Environment (CE): Reference the launch template; match the same AZ and instance type as the reservation
- Allocation strategy: BEST_FIT
- Create a Job Queue and attach the CE
- Submit jobs ahead of time; Batch will start them when the window opens

## Important Considerations
- Single‑use CE: After the reservation expires, the CE becomes invalid—delete and recreate for the next block
- Scaling behavior:
  - minvCpus = 0: Batch waits for the window, then launches instances
  - minvCpus > 0: Batch still waits for the window; may pre‑stage differently
- Multi‑Node Parallel (MNP) jobs: Set maxvCpus to the total reserved capacity so all nodes can launch together

## Alternatives
- On‑Demand Capacity Reservations (ODCR): Flexible reservations for mission‑critical, usually non‑GPU workloads; can be grouped and reused
- Spot Instances: For single‑node, interruption‑tolerant jobs (e.g., P5 Spot) with potential savings up to ~75%

## Key Takeaways
- CBML guarantees GPUs at the exact time you need them; Batch automates starting/stopping within the window
- Treat CBML compute environments as disposable; rebuild per reservation
- Validate AZ, instance types, and caps (min/max vCPUs) to align with your reserved capacity
- Use ODCR or Spot where they better fit reliability/cost trade‑offs

## Conclusion
Combining Capacity Blocks with AWS Batch lets you automate high‑performance ML training on reserved GPUs—ensuring you utilize the capacity you paid for, exactly when scheduled, with minimal operational overhead.
