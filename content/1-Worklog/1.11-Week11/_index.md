---
title: "Week 11 Worklog"
date: "2025-10-22T03:10:22Z"
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:

* Design and implement a hybrid recommendation architecture (Real-time + Batch-inference) for Rafilm.
* Stabilize event ingestion (putEvents/putItems) and nightly batch pipeline with SAM.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                                      | Date       | Completion Date | Reference Material                                                                                 |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | --------------------------------------------------------------------------------------------------- |
| 2   | - Architecture consolidation: define data flow between API Gateway → Lambda → Personalize (Realtime) and S3 → Personalize Batch → DynamoDB (Cache) <br> - Document component boundaries and error-handling strategy     | 11/17/2025 | 11/17/2025      | https://docs.aws.amazon.com/personalize/latest/dg/recording-events.html                            |
| 3   | - Implement realtime event tracking: integrate `PutEvents` and `PutItems` into Lambda behind API Gateway <br> - Add request validation, retries, and structured logging                                                   | 11/18/2025 | 11/18/2025      | https://docs.aws.amazon.com/personalize/latest/dg/API_UBS_PutEvents.html                           |
| 4   | - Enhance batch pipeline: schedule batch-inference (EventBridge) → Personalize → write outputs to S3 → transform to DynamoDB cache <br> - Add de-duplication and idempotent writes                                       | 11/19/2025 | 11/19/2025      | https://docs.aws.amazon.com/personalize/latest/dg/batch-inference.html                             |
| 5   | - Lambda optimization: split handlers (realtime vs batch ETL), reduce cold starts, add concurrency and backoff controls <br> - Implement feature flags to switch between realtime and cached responses                   | 11/20/2025 | 11/20/2025      | https://aws.amazon.com/blogs/compute/optimizing-node-js-dependency-management-in-aws-lambda/       |
| 6   | - End-to-end testing: simulate user traffic, verify recommendation freshness and fallback <br> - Cost/performance review and finalize documentation                                                                      | 11/21/2025 | 11/21/2025      | https://aws.amazon.com/personalize/pricing/                                                         |

### Week 11 Achievements:

**Objective 1**: Hybrid Architecture Design (Realtime + Batch)

✅ Finalized a dual-path recommendation flow:
- Realtime path: API Gateway → Lambda (PutEvents/PutItems) → Personalize Campaign (GetRecommendations).
- Batch path: Nightly EventBridge schedule → Personalize Batch Inference → S3 output → Lambda ETL → DynamoDB cache.

**Objective 2**: Robust Ingestion & Caching

✅ Implemented event validation, structured logging, and retries for realtime ingestion.  
✅ Built idempotent batch ETL with de-duplication to keep DynamoDB cache consistent and avoid write-amplification.

**Objective 3**: Operational Cleanliness

✅ Separated Lambda handlers for clarity and scalability; tuned memory/timeouts and enabled reserved concurrency.  
✅ Added feature flags to route requests: prefer realtime; fallback to cached DynamoDB when campaign is throttled or offline.

**Key outcomes**:
+ Freshness vs. Stability: Realtime delivers up-to-the-moment recommendations; batch ensures broad coverage and low-latency reads via cache.  
+ Resilience: Fallback logic guarantees service continuity using cached results when realtime is degraded.  
+ Cost control: EventBridge scheduling and DynamoDB TTL reduce unnecessary recomputation and storage.  
+ Observability: Centralized logs/metrics (duration, errors, cache hit rate) support performance tuning and incident response.

