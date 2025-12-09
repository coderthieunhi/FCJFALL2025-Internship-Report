---
title: "Week 10 Worklog"
date: "2025-10-22T03:10:22Z"
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---



### Week 10 Objectives:

* Implement Personalize to Rafilm project


### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - **Batch-inference implementation** :<br> create necessary resources in SAM :<br> + Dynamo cache table, S3<br> - **Optimizing lambda function for triggering batch -inference**                                                                                       | 11/10/2025 | 11/10/2025      | https://docs.aws.amazon.com/personalize/
| 3   |- **Debugging** :<br> + Debug batch-job failed due to mismatch path in cloudformation template<br> + Debug redundant batch-job creation<br> + Debug mismatch user-id in batch-output dynamodb table                                       | 11/11/2025 | 11/11/2025      |https://docs.aws.amazon.com/personalize/|
| 4   | - **Research realtime campaign features** :focus on putevents and putitems | 11/12/2025 | 11/12/2025      | https://github.com/aws-samples/amazon-personalize-samples <br> |
| 5   |- Implement putitems and putevents into lambda function for event tracking | 11/13/2025 | 11/13/2025      | https://aws.amazon.com/personalize/pricing/
| 6   |- Refactor for clean code, add explaintory comments <br>  | 11/14/2025 | 11/14/2025      | 

### Week 10 Achievements:


**Key outcomes**:



+ Ready Batch Pipeline: Successfully implemented a stable, automated batch recommendation system using SAM, Lambda, S3, and DynamoDB.

+ Troubleshoot successfully integration issues across CloudFormation, Personalize, and data layers.

+ Real-Time Capability Expansion: Enhanced the recommendation engine with live event tracking, allowing for more responsive and personalized suggestions.

+ Code Quality Improvement: Applied clean code principles through refactoring, resulting in a more scalable and maintainable codebase.

+ Cost & Performance Awareness: Optimized Lambda execution and eliminated redundant jobs to improve efficiency and control costs.