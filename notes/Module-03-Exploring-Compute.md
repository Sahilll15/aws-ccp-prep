# Module 3 — Exploring Compute Services

**Status: ✅ done** · Domain 3 · Full notes in the [Study hub](AWS-Cloud-Practitioner.html) → Domain 3 Compute.

## Key points
- **Serverless** = no servers to provision/manage; AWS handles scaling/patching/availability; **pay only when running**.
- **AWS Lambda** — event-driven functions (S3/API Gateway/SQS/schedule triggers); pay per request + ms; **$0 idle**; **15-min max** per run → short tasks.
- **Containers**: app + deps packaged (Docker), share host kernel → lighter than VMs.
  - **ECS** (AWS-native orchestration) · **EKS** (managed Kubernetes) · **Fargate** (serverless — no EC2 hosts) · **ECR** (image registry).
- **Additional compute**: **Elastic Beanstalk** (PaaS — upload code, auto LB/scaling) · **Lightsail** (simple cheap VPS) · **Batch** (large batch jobs) · **Outposts** (AWS hardware on-prem / hybrid).

> Pick-the-compute: full OS control → EC2 · fast web app → Beanstalk · simple site → Lightsail · containers → ECS/EKS (+Fargate to skip servers) · short event code → Lambda.
