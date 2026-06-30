# Module 12 — Migrating to the AWS Cloud

**Status: ⬜ upcoming** · Domain 1 (Cloud Concepts) · We'll deepen this and build a visual page when we study it.

## AWS Cloud Adoption Framework (CAF)
Guidance for planning a cloud migration, organized into **6 perspectives**:
- **Business · People · Governance** (people/org side)
- **Platform · Security · Operations** (technical side)
- Benefits: reduce business risk · improve ESG/compliance · grow revenue · increase operational efficiency.

## Migration strategies — the "6 R's"
- **Rehost** — "lift and shift" (move as-is, fastest).
- **Replatform** — "lift, tinker, and shift" (small optimizations, e.g. move DB to RDS).
- **Repurchase** — drop and buy a SaaS replacement.
- **Refactor / Re-architect** — rewrite for cloud-native (most effort, most benefit).
- **Retire** — decommission what's no longer needed.
- **Retain** — keep on-prem for now (not ready to move).

## Data transfer / migration tools
- **AWS Snow Family** — **Snowcone / Snowball Edge / Snowmobile** — physically ship large data when the network is too slow.
- **AWS DataSync** — automated online data transfer to AWS.
- **AWS Transfer Family** — SFTP/FTPS transfers into S3/EFS.
- **AWS Migration Hub** — track migrations in one place. **DMS** — migrate databases (see Module 7).

## Likely exam framing
- "Plan an org-wide cloud adoption" → **CAF (6 perspectives)**.
- "Move app as-is, fast" → **Rehost**. "Minor tweaks during move" → **Replatform**. "Switch to SaaS" → **Repurchase**.
- "Ship 100 TB, slow internet" → **Snowball**; petabytes/exabytes → **Snowmobile**.
