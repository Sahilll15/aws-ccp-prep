# Module 11 — Pricing and Support

**Status: ⬜ upcoming** · Domain 4 (Billing, Pricing & Support — 12%) · We'll deepen this and build a visual page when we study it.

## Pricing fundamentals
- **3 cost drivers**: **compute**, **storage**, **data transfer** (data **in** is usually free; data **out** is charged).
- **Pay-as-you-go**; commit (Reserved/Savings Plans) for discounts; **volume discounts** (pay less per unit as you use more).
- **AWS Free Tier**: **always free** (e.g. Lambda 1M req/mo) · **12-month free** (e.g. 750 hrs t2.micro) · **trials** (short-term).

## Billing & cost-management tools
- **AWS Pricing Calculator** — estimate costs **before** building.
- **AWS Budgets** — set spend/usage limits + alerts (proactive).
- **AWS Cost Explorer** — visualize/analyze **past** spend + forecast.
- **Cost & Usage Report (CUR)** — most detailed billing data.
- **Cost allocation tags** — attribute costs to teams/projects.
- **AWS Organizations** + **Consolidated Billing** — one bill for many accounts + shared volume discounts.

## Support plans (know the ladder)
- **Basic** (free) — docs, forums, Trusted Advisor (core checks).
- **Developer** (~$29/mo) — business-hours email, experimenting.
- **Business** (~$100/mo) — 24/7 phone/chat, **full Trusted Advisor**; min for production.
- **Enterprise On-Ramp** (~$5,500/mo) — pool of TAMs, faster response.
- **Enterprise** (~$15,000/mo) — dedicated **Technical Account Manager (TAM)**, 15-min critical response, Concierge.

## Likely exam framing
- Estimate before building → **Pricing Calculator** · alert on spend → **Budgets** · analyze past spend → **Cost Explorer** · one bill many accounts → **Organizations/Consolidated Billing** · dedicated **TAM** → **Enterprise** plan.
