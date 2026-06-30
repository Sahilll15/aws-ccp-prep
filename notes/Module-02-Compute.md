# Module 2 — Compute in the Cloud

**Status: ✅ done** · Domain 3 · Full notes in the [Study hub](AWS-Cloud-Practitioner.html) → Domain 3 Compute.

## Key points
- **Amazon EC2** — resizable virtual servers. Default tenancy = **shared/multi-tenant** (isolated by the Nitro hypervisor). Single-tenant options: Dedicated Instances, Dedicated Hosts (BYOL).
- **Instance families**: general purpose · compute optimized · memory optimized · storage optimized · accelerated (GPU).
- **EC2 pricing** (heavily tested): **On-Demand** (default, spiky) · **Reserved Instances** (1–3 yr commit, steady) · **Savings Plans** (commit $/hr, flexible) · **Spot** (~90% off, interruptible) · **Dedicated Hosts** (licensing).
- **EC2 Auto Scaling** = elasticity (add/remove instances to match demand).
- **Elastic Load Balancing (ELB)** = spreads traffic → high availability; pairs with Auto Scaling.
- **Messaging**: **SQS** = queue, pull-based, decouple components · **SNS** = pub/sub topic, push-based, fan-out.

> Exam: **Spot** = cheapest but interruptible · **RI / Savings Plans** = commit for discount · **SQS = queue (pull)**, **SNS = pub/sub (push)**.
