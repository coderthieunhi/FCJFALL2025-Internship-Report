---
title: "Week 9 Worklog"
date: "2025-10-22T03:10:22Z"
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---



### Week 9 Objectives:

* Implement Personalize to Rafilm project


### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - **Preparing dataset** :<br> Research for dataset (MoviesLen dataset selection)<br> - Format the dataset to match Personalize requirements                                                                                        | 11/03/2025 | 11/03/2025      | https://grouplens.org/datasets/movielens/
| 3   |- **Launch demo campaigns** :<br> + Define schema, create solution                                       | 11/04/2025 | 11/04/2025      |https://docs.aws.amazon.com/personalize/latest/dg/API_Campaign.html|
| 4   | - **Writing Lambda Function** :<br> Functions to handle result from campaign  Amazon Personalize| 11/05/2025 | 11/05/2025      | https://github.com/aws-samples/amazon-personalize-samples <br> |
| 5   |- Research cost optimization for Amazon Personalize<br> | 11/06/2025 | 11/06/2025      | https://aws.amazon.com/personalize/pricing/
| 6   |- **Writing Lambda Function** <br> :Functions to handle and trigger batch-inference | 11/07/2025 | 11/07/2025      | 

### Week 9 Achievements:


**Key outcomes**:

+ Dataset Acquisition & Preparation: Successfully researched and selected the MovieLens dataset for the recommendation engine, then formatted and structured it to meet Amazon Personalize's schema requirements (Users, Items, Interactions).

+ Personalize Campaign Implementation: Gained hands-on experience with Amazon Personalize by defining schemas, creating a solution version, and launching a live demo campaign, establishing a functional recommendation model.

+ Lambda Integration Development: Built and tested AWS Lambda functions to interact with the Personalize campaign, enabling the backend to fetch real-time recommendations based on user input.

+ Cost-Aware Architecture Planning: Researched Amazon Personalize pricing and optimization strategies, ensuring the project remains cost-effective while scaling—covering training, inference, and real-time recommendation costs.

+ Batch Inference Pipeline Initiation: Began developing Lambda functions to trigger and handle batch inference jobs, moving toward scalable, scheduled recommendation updates for all users.
