# Module 10 — Monitoring, Compliance and Governance

**Status: ⬜ upcoming** · Domains 2 & 3 · We'll deepen this and build a visual page when we study it.

## Core services (commonly confused — nail the distinction)
- **Amazon CloudWatch** — **monitoring**: metrics, **alarms**, logs, dashboards. Answers *"is it healthy / how is it performing?"*
- **AWS CloudTrail** — **audit log of API calls**: who did what, when, from where. Answers *"who made this change?"* (governance/forensics).
- **AWS Config** — tracks **resource configuration** over time + checks against **compliance rules**. Answers *"is this resource configured correctly / what changed?"*
- **AWS Trusted Advisor** — automated **best-practice checks** across 5 categories: **cost optimization, security, fault tolerance, performance, service limits**.
- **AWS Audit Manager** — automates evidence-gathering for audits.
- **AWS Health Dashboard** — status of AWS services + events affecting your account.

## Likely exam framing
- "**Performance/metrics/alarms**" → **CloudWatch**.
- "**Who made an API call / audit trail**" → **CloudTrail**.
- "**Resource configuration / compliance over time**" → **AWS Config**.
- "**Best-practice recommendations** (cost/security/limits)" → **Trusted Advisor**.

> Memory hook: **CloudWatch = watch performance · CloudTrail = trail of who-did-what · Config = configuration compliance.**
