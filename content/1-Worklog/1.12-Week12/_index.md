---
title: "Week 12 Worklog"
date: "2025-10-22T03:10:22Z"
weight: 2
chapter: false
pre: " <b> 1.12. </b> "
---

### Week 12 Objectives:

* Finalize: sync user data from DynamoDB into Personalize datasets (Items, Interactions).
* Merge code, resolve conflicts, test full Personalize (realtime + batch), and complete docs/deployment.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                                         | Date       | Completion Date | Reference Material                                                                                 |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | --------------------------------------------------------------------------------------------------- |
| 2   | - Design ETL sync flow: DynamoDB (Users/Ratings) → S3 (CSV/JSON) → Personalize Datasets (Items, Interactions) <br> - Normalize schema/mapping (userId, itemId, timestamp, eventType)                                       | 11/24/2025 | 11/24/2025      | https://docs.aws.amazon.com/personalize/latest/dg/datasets-and-schemas.html                        |
| 3   | - Implement Lambda ETL: paginate DynamoDB scan, transform data, write to S3 by partition/date <br> - Add idempotency, de-duplication, and data validation                                                                   | 11/25/2025 | 11/25/2025      | https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/dynamodb-example-table-read.html |
| 4   | -  Demo Import/Update Personalize datasets: Items + Interactions <br> - Trigger re-train/re-deploy on manual for demo                                                                             | 11/26/2025 | 11/26/2025      | https://docs.aws.amazon.com/personalize/latest/dg/recording-events.html                            |
| 5   | - Code merge to main: resolve conflicts in SAM templates and Lambda handlers (realtime/batch/etl) <br> - Set up CI for lint/build/test on PR                                                                                | 11/27/2025 | 11/27/2025      | https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html    |
| 6   | - End-to-end testing: <br> Realtime (PutEvents/PutItems → GetRecommendations) <br> Batch (ETL → Batch Inference → DynamoDB Cache → Fallback) <br> - Cost/perf review, finalize docs and handover checklist                  | 11/28/2025 | 11/28/2025      | https://aws.amazon.com/personalize/pricing/                                                        |

### Week 12 Achievements:

**Objective 1**: Sync user data into Personalize  
✅ Completed ETL pipeline from DynamoDB to S3 with daily partitions and normalized Items/Interactions schema.  
✅ Automated dataset import/update and triggered re-train/re-deploy when data changed substantially.

**Objective 2**: Merge & conflict resolution  
✅ Merged feature branches to main; resolved conflicts in CloudFormation/SAM and Lambda (realtime, batch, etl).  
✅ Established CI to run lint, build, and tests before deployment.

**Objective 3**: Full Personalize testing (hybrid)  
✅ Realtime: verified PutEvents/PutItems and user-specific GetRecommendations.  
✅ Batch: executed batch inference, populated DynamoDB cache, validated fallback when campaign throttled/offline.  
✅ Metrics captured: latency, errors.

**Key outcomes**:
+ Reliable data sync: Items/Interactions updated from DynamoDB on schedule, keeping recommendations fresh.  
+ Stable hybrid architecture: Realtime for immediacy; batch for broad coverage and low-latency cache reads.  
+ Operational efficiency: Optimized ETL/Lambda and documented processes with a complete handover checklist.