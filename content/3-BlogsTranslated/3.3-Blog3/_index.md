---
title: "Blog 3"
date: "2025-10-22T03:10:22Z"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---


**FULL VIETNAMESE TRANSLATED BLOG:** [Các phương pháp tốt nhất để tận dụng AWS Systems Manager với AWS Fault Injection Service](https://docs.google.com/document/d/1VPZj-1wk8V3aKY13bVzHVr4j5fdVZIgYAgrMk78rux8/edit?usp=sharing)  
**ORIGINAL BLOG:** [Best practices for utilizing AWS Systems Manager with AWS Fault Injection Service](https://aws.amazon.com/vi/blogs/mt/best-practices-for-utilizing-aws-systems-manager-with-aws-fault-injection-service/)

# Summary: Best practices for utilizing AWS Systems Manager with AWS Fault Injection Service

This post explains how combining AWS Systems Manager (SSM) with AWS Fault Injection Service (FIS) enables broader, safer, and more realistic chaos engineering experiments for applications ranging from custom stacks to SAP.

## Why integrate SSM with FIS?
- Expanded capabilities: Use SSM’s aws:ssm:send-command to run Bash/PowerShell on targets, enabling precise, complex fault scenarios beyond built‑in FIS actions.
- Centralized control: Target SSM‑managed nodes (EC2, on‑prem, edge) across accounts/regions from a single experiment.

## Best practices for SSM documents
- Modular structure: Split documents into steps: validate prerequisites → inject fault → clean up. Improves troubleshooting and rollback.
- Clear parameters: Define types, descriptions, allowed patterns/ranges (e.g., app/service names) to prevent misuse.
- Environment variables: Avoid hardcoding regions/IDs. Use built‑in variables (e.g., AWS_SSM_REGION_NAME) to keep scripts portable.
- OS detection: Auto‑detect platform (Amazon Linux/Ubuntu/Windows) and branch to appropriate commands/package managers.
- Preconditions: Gate steps on platform or dependency checks; skip or fail fast if requirements aren’t met.
- Failure handling: Use OnFailure: exit so the experiment stops and reports failure instead of leaving systems indeterminate.
- Idempotency: Check state before acting (e.g., only stop a service if running) to allow safe retries/resumes.
- Timeouts: Set timeoutSeconds per step; terminate hung scripts and trigger clean‑up to restore baseline.
- Logging: Emit verbose logs (echo/Write‑Output). Ship execution logs to CloudWatch Logs or S3 for analysis and audits.

## Typical experiment flow
1) Validate: Confirm target platform, required agents/packages, and permissions.  
2) Inject fault: Run controlled failure (CPU/memory pressure, service stop, latency, packet loss).  
3) Observe: Verify detection and alerts (CloudWatch/alerts runbooks).  
4) Clean up: Revert changes, restart services, and confirm healthy state.

## Key takeaways
- SSM + FIS increases experiment fidelity while maintaining safety through parameters, preconditions, and strict failure/timeout controls.
- Portability and reuse come from modular documents, OS‑aware scripting, and environment‑based configuration.
- Strong observability and logging are essential to validate resilience and to learn from experiments.
- Idempotent, time‑bounded steps prevent drift and simplify rollback during chaos tests.