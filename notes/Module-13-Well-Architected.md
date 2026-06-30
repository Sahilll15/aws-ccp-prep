# Module 13 — Well-Architected Solutions

**Status: ⬜ upcoming** · Domain 1 (Cloud Concepts) · We'll deepen this and build a visual page when we study it.

## The AWS Well-Architected Framework — 6 pillars
Best-practice guidance for building on AWS. Mnemonic **O-S-R-P-C-S**:
1. **Operational Excellence** — run and monitor systems; continuously improve processes.
2. **Security** — protect data and systems (confidentiality, integrity, least privilege).
3. **Reliability** — recover from failure, scale to meet demand (HA, backups, multi-AZ).
4. **Performance Efficiency** — use resources efficiently; pick the right resource for the job.
5. **Cost Optimization** — avoid unnecessary cost; pay only for what you need.
6. **Sustainability** — minimize the environmental impact of workloads.

## Supporting
- **AWS Well-Architected Tool** — free console tool to review a workload against the pillars and get improvement recommendations.
- **Design principles** (recurring themes): stop guessing capacity · automate · design for failure · scale horizontally · decouple components · use managed services.

## Likely exam framing
- Given a scenario, identify **which pillar** it serves: "recover from failure / multi-AZ" → **Reliability**; "least privilege / encryption" → **Security**; "right-size to cut spend" → **Cost Optimization**; "reduce carbon footprint" → **Sustainability**.

> Don't confuse the **6 pillars** (this module) with the **6 advantages of cloud** (Module 1) — different lists, both tested.
