# Module 11 — Billing, Pricing & Support

**Status: ✅ done (in depth)** · Domain 4 (12%) · Visual page: [Billing & Pricing](../billing-and-pricing.html). The smallest domain and the easiest points — concrete recall, not concepts. Bank all of it. Whole domain = **4 pillars**: how you're charged · tools to see/control cost · billing across accounts · support plans.

## Pillar 1 — How AWS charges you
Utility model (like electricity): pay for what you draw, better rates if you commit. **Three pricing principles:**
- **Pay as you go** — only for what you use, no big upfront, no long contracts required.
- **Save when you commit** — Reserved Instances / Savings Plans → big discount for 1–3 yr commitment.
- **Pay less as AWS grows** — economies of scale + tiered/volume discounts → more usage, lower per-unit price.

**Three cost drivers** (what you actually pay for): **Compute · Storage · Data transfer.**
> **Gotcha:** data **IN** is generally **free**; data **OUT** to the internet **costs**; same-Region transfer usually free/cheap. "What's expensive?" → moving data *out*.

### Free Tier — 3 flavors
- **Always Free** — free forever within limits (Lambda 1M req/mo, DynamoDB 25 GB).
- **12 Months Free** — free for first 12 months after sign-up (750 hrs/mo t2.micro EC2, 5 GB S3).
- **Trials** — short-term, starts when you activate the service (some SageMaker/Inspector).

## Pillar 2 — The four cost tools (most-tested; keep them straight by *when in time*)
| Tool | When | Job |
|---|---|---|
| **Pricing Calculator** | Before | **Estimate** an architecture's cost *before* building (planning). |
| **AWS Budgets** | Watching | Set spend/usage limits, get **alerts** when you cross / are forecast to cross. Proactive. |
| **Cost Explorer** | After | **Visualize & analyze** past/current spend, trends, forecast. "Where did money go?" |
| **Cost & Usage Report (CUR)** | Raw | **Most detailed** line-item/hourly billing data, exported to S3 for deep analysis. |

> Analogy: Calculator = the quote before the job · Budgets = the smoke alarm · Cost Explorer = your bank statement review · CUR = the itemized receipt.
> **Cost allocation tags** — tag resources (`team:marketing`) to break spend down by team/project/env in Cost Explorer/CUR.

## Pillar 3 — Many accounts → one bill
**AWS Organizations** = centrally manage many AWS accounts. Billing superpower = **Consolidated Billing**:
- **One bill** for all accounts (one payer account).
- **Combined usage → bigger volume discounts**, pooled and shared across accounts.
- Easier tracking + central governance (SCPs, more of a security topic).
> Trigger: "one bill for multiple accounts" / "share volume discounts" → **Organizations + Consolidated Billing**.

## Pillar 4 — The support-plan ladder
Learn **what each tier unlocks** (that's how questions are phrased), not exact prices.
| Plan | ~Price | Unlocks (tested bits) |
|---|---|---|
| **Basic** | Free | Docs, forums, 24/7 account/billing customer service, **core** Trusted Advisor checks, Health Dashboard. No tech support. |
| **Developer** | ~$29/mo | Email support, **business hours**, 1 contact. Experimenting/dev. |
| **Business** | ~$100/mo | **24/7 phone/chat/email** with engineers, **full Trusted Advisor**, unlimited contacts, 3rd-party software support. **Min for production.** |
| **Enterprise On-Ramp** | ~$5,500/mo | **Pool of TAMs**, <30 min business-critical response, cost-optimization workshops. |
| **Enterprise** | ~$15,000/mo | **Designated TAM**, **<15 min** business-critical response, Concierge, Incident Detection & Response, Well-Architected reviews. |

> Triggers: "free/just starting" → **Basic** · "24/7 phone" or "full Trusted Advisor" → **Business** (production minimum) · "**designated** TAM / <15 min" → **Enterprise** · "**pool** of TAMs" → **On-Ramp**.

## Bonus — AWS Trusted Advisor (shows up in billing Qs)
Automated best-practice checks in **5 categories**: **Cost Optimization** (find idle/underused resources), **Security**, **Fault Tolerance**, **Performance**, **Service Limits**. Basic/Developer = core checks only; **Business+ = all checks**.

## Exam-trigger cheat sheet
- estimate before building → **Pricing Calculator** · alert on spend → **Budgets** · analyze past spend → **Cost Explorer** · line-item detail → **CUR**
- one bill, many accounts, volume discounts → **Organizations / Consolidated Billing** · cost by team → **cost allocation tags**
- 24/7 phone + full Trusted Advisor (prod) → **Business** · designated TAM / 15-min → **Enterprise** · find idle resources → **Trusted Advisor (Cost Optimization)**
- free forever (limits) → **Always Free** · first 12 months → **12 Months Free**
