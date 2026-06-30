# ☁️ AWS Certified Cloud Practitioner (CLF-C02)

Study hub for the **AWS Certified Cloud Practitioner** exam. Goal: **pass in ~2–3 weeks (intensive)**. Mode: Claude teaches → structured notes land here as we go. This is a **conceptual** exam — **no Linux / CLI / hands-on required**.

> 📋 **Complete topic checklist + Skill Builder module breakdown:** [[AWS-CLF-C02-Study-Guide]] — every objective as a tickable to-do, converted from Hiroko Nishimura's CLF-C02 guide, mapped to the AWS Skill Builder courses I'm using.

← back to [[DevOps]]

---

## 🎯 Exam at a glance

| | |
|---|---|
| Exam code | **CLF-C02** (current version) |
| Questions | **65** (multiple choice + multiple response) |
| Time | **90 minutes** |
| Pass mark | **700 / 1000** (scaled) |
| Cost | **~$100 USD** |
| Format | Online proctored or test center |
| Level | Foundational — breadth, not depth. No hands-on. |
| 🎯 **Target exam date** | **Saturday, 18 July 2026** (booked target — reschedulable free up to 24h before) |

> **Readiness gate:** don't sit it until you're scoring **80%+** on practice exams. That score — not the calendar — is the real go signal. Slide the date if you're not there by ~14 Jul.

### The 4 domains (memorize these weights)

| # | Domain | Weight | Status |
|---|--------|--------|--------|
| 1 | **Cloud Concepts** | 24% | ◐ in progress |
| 2 | **Security & Compliance** | 30% | ⬜ |
| 3 | **Cloud Technology & Services** | 34% | ◐ in progress (Compute ✅, Global infra ✅, Networking ✅) |
| 4 | **Billing, Pricing & Support** | 12% | ⬜ |

> **Head start:** [[Networking]] already covers VPC, subnets, security groups, Route 53 (DNS), and load balancers — a big chunk of Domain 3's networking. The hands-on VPC/subnet/peering you did transfers directly.

---

## 🗓️ 2–3 week intensive plan

**📆 Start: Sun 28 Jun 2026 · Exam: Sat 18 Jul 2026 (20 days).** Plan has 15 study days across 20 calendar days — built-in slack for rest/catch-up. Week ranges below; key milestone = practice-exam-ready by **~14 Jul**.

**Week 1 (Jun 28 – Jul 4) — Concepts + Security (the foundation + the heaviest domain)**
- [x] Day 1 — Cloud Concepts: what cloud is, 6 advantages, IaaS/PaaS/SaaS, deployment models, Well-Architected
- [ ] Day 2 — AWS Global Infrastructure (Regions / AZs / Edge) + ways to access AWS (Console/CLI/SDK)
- [ ] Day 3 — **Shared Responsibility Model** + AWS IAM (users, groups, roles, policies, MFA, root)
- [ ] Day 4 — Security services (Shield, WAF, GuardDuty, Inspector, Macie, KMS, Secrets Manager)
- [ ] Day 5 — Compliance & governance (Artifact, Config, CloudTrail, Organizations/SCPs)
- [ ] Day 6 — Review Domains 1–2 + practice questions

**Week 2 (Jul 5 – Jul 11) — Core Services + Billing**
- [ ] Day 7 — Compute (EC2 + instance/pricing types, ELB, Auto Scaling, Lambda, ECS/EKS/Fargate, Beanstalk, Lightsail)
- [ ] Day 8 — Storage (S3 + classes, EBS, EFS, FSx, Storage Gateway, Snow family)
- [ ] Day 9 — Networking (VPC ✅, Route 53, CloudFront, Direct Connect, VPN) + Databases (RDS, Aurora, DynamoDB, Redshift, ElastiCache)
- [ ] Day 10 — Management & monitoring (CloudWatch, CloudTrail, CloudFormation, Trusted Advisor, Systems Manager) + integration (SNS, SQS)
- [ ] Day 11 — Billing, Pricing & Support (pricing models, Free Tier, Cost Explorer, Budgets, Organizations, support plans)
- [ ] Day 12 — Review Domains 3–4 + practice questions

**Week 3 (Jul 12 – Jul 17) — Exam readiness (buffer)**
- [ ] Day 13 — Full practice exam #1 → review weak areas
- [ ] Day 14 (~Jul 14) — Full practice exam #2 → **must be hitting 80%+ here**
- [ ] Day 15 (Jul 15–17) — Final cheat-sheet review

**🎯 Sat 18 Jul 2026 — SIT THE EXAM**

---

## Domain 1 — Cloud Concepts (24%)

### What is cloud computing?
**On-demand delivery of IT resources (compute, storage, databases, networking) over the internet, with pay-as-you-go pricing.** Instead of buying, owning, and maintaining physical servers and data centers, you rent them from a provider (AWS) and pay only for what you use.

- **Provision in minutes**, not weeks of procurement.
- **Pay-as-you-go** — like electricity: use it, pay for it; stop, stop paying.
- AWS owns/operates the hardware; you consume it as a service.

### Client–server model (Module 1 basics)
- **Client** = a web browser or app a person interacts with. **Server** = e.g. an **Amazon EC2** instance.
- Flow: client makes a **request** → server **evaluates** → server **responds**. This is the basic shape of how AWS services communicate.
- *Exam tip:* don't confuse **deployment models** (cloud / hybrid / on-prem = *where it runs*) with **service models** (IaaS / PaaS / SaaS = *who manages what*) — different axes, both tested.

### The 6 advantages of cloud (AWS's official list — common exam Q)
1. **Trade capital expense for variable expense** — no big upfront server purchase (CapEx → OpEx); pay as you consume.
2. **Benefit from massive economies of scale** — AWS's huge scale → lower pay-as-you-go prices than you'd get alone.
3. **Stop guessing capacity** — scale up/down on demand; no over- or under-provisioning.
4. **Increase speed and agility** — new resources in minutes → experiment and ship faster.
5. **Stop spending money running and maintaining data centers** — focus on your product, not racking servers.
6. **Go global in minutes** — deploy across AWS Regions worldwide to be close to users.

> **Mnemonic — "Very Easy Cloud Saves Data Globally":** **V**ariable expense · **E**conomies of scale · **C**apacity (stop guessing) · **S**peed/agility · **D**ata centers (stop maintaining) · **G**lobal in minutes. *Don't confuse these 6 advantages of cloud with the 6 Well-Architected pillars (O-S-R-P-C-S) — different list, both tested.*

### Cloud service models — *who manages what*
| Model | What it is | You manage | Examples |
|---|---|---|---|
| **IaaS** (Infrastructure) | Raw building blocks (VMs, storage, network) | OS, runtime, app, data | EC2, VPC, EBS |
| **PaaS** (Platform) | Managed platform to run apps | Just your app + data | Elastic Beanstalk, RDS, Lambda |
| **SaaS** (Software) | Finished software, ready to use | Nothing (just use it) | Gmail, Salesforce, Dropbox |

> Mnemonic: IaaS = you get the *kitchen*, PaaS = you get the *kitchen + appliances*, SaaS = you get the *meal*.

### Cloud deployment models
- **Cloud (public)** — everything runs in the cloud (AWS). Most common for new apps.
- **Hybrid** — mix of cloud + on-premises (e.g. keep a legacy DB on-prem, run the app in AWS). Connected via VPN/Direct Connect.
- **On-premises / private cloud** — run in your own data center (sometimes with cloud-like tooling). Full control, full cost/maintenance.

### Cloud economics
- **CapEx vs OpEx** — cloud shifts big upfront capital spend (CapEx) to ongoing operating spend (OpEx) you only pay for what you use.
- **Economies of scale** — AWS buys hardware at massive volume → cheaper per unit → passed to you.
- **TCO (Total Cost of Ownership)** — cloud often lowers TCO (no data-center real estate, power, cooling, hardware refresh, ops staff).

### AWS Well-Architected Framework — the **6 pillars**
Best-practice guidance for building on AWS (exam loves these):
1. **Operational Excellence** — run & monitor systems, improve processes
2. **Security** — protect data & systems
3. **Reliability** — recover from failure, scale to meet demand
4. **Performance Efficiency** — use resources efficiently as needs change
5. **Cost Optimization** — avoid unnecessary cost
6. **Sustainability** — minimize environmental impact

> Mnemonic: **"O-S-R-P-C-S"** → *Operational, Security, Reliability, Performance, Cost, Sustainability.*

---

## Domain 2 — Security & Compliance (30%)
<!-- Day 3-5. Shared Responsibility Model (AWS = security OF the cloud; you = security IN the cloud). IAM: users/groups/roles/policies, MFA, root account best practices, least privilege. Security svcs: Shield (DDoS), WAF (L7), GuardDuty, Inspector, Macie, KMS, Secrets Manager, Cognito. Compliance: Artifact, Config, CloudTrail, Organizations/SCPs. -->

## Domain 3 — Cloud Technology & Services (34%)

### Compute — Skill Builder Module 2 ✅ *(done 29 Jun 2026)*

**Amazon EC2** — resizable virtual servers ("instances") in the cloud; you choose OS, instance size, and networking.
- **Tenancy:** default is **shared / multi-tenant** — instances from many AWS customers share the same physical hardware, kept isolated by the **Nitro hypervisor**. This sharing → *economies of scale* → low, pay-as-you-go cost.
- Pay more for single-tenant when compliance/licensing demands it: **Dedicated Instances** (hardware isolated to your account) or **Dedicated Hosts** (a whole physical server you control — for BYOL per-socket/core licensing).

**Instance families** (match the instance to the workload):
- **General purpose** — balanced (web servers, small DBs)
- **Compute optimized** — CPU-heavy (batch, gaming, HPC)
- **Memory optimized** — large in-memory work (big DBs, caches)
- **Storage optimized** — high disk throughput (data warehousing)
- **Accelerated computing** — GPUs (ML, graphics)

**EC2 pricing models** (heavily tested):
| Model | What | Best for |
|---|---|---|
| **On-Demand** | Pay per second/hour, no commit | Spiky / short / unpredictable; default |
| **Reserved Instances (RI)** | 1- or 3-yr commit → big discount | Steady, predictable usage |
| **Savings Plans** | Commit to $/hr for 1–3 yrs → discount, more flexible than RIs | Predictable spend, want flexibility |
| **Spot Instances** | Up to ~90% off unused capacity; AWS can reclaim w/ 2-min notice | Fault-tolerant, flexible (batch, CI) |
| **Dedicated Hosts** | Whole physical server for you | Licensing / compliance |

**EC2 Auto Scaling** — automatically adds/removes instances to match demand = **elasticity** (dynamic + predictive scaling).
**Elastic Load Balancing (ELB)** — distributes incoming traffic across instances/targets → **high availability + fault tolerance**; single regional point of contact. Pairs with Auto Scaling.

**Messaging & queuing** (decouple components → monolith to microservices):
- **Amazon SQS** (Simple Queue Service) — messages sit in a **queue** until a consumer pulls + processes them; sender/receiver decoupled, nothing lost if consumer is busy. **Pull**-based.
- **Amazon SNS** (Simple Notification Service) — **pub/sub**: publish to a **topic** → fan-out to many subscribers (email, SMS, Lambda, SQS). **Push**-based.

**Serverless — AWS Lambda** — run code with **no servers to manage**; event-driven; pay only for compute time used; 15-min max per invocation.

**Containers:** **Amazon ECS** (AWS container orchestration) · **Amazon EKS** (managed Kubernetes) · **AWS Fargate** (**serverless** engine — run containers without managing the EC2 hosts).

> **Exam framing:** EC2 = *you* manage the server; **Lambda / Fargate = serverless** (AWS manages it). **Spot** = cheapest but interruptible; **RI / Savings Plans** = commit for a discount. **SQS = queue (pull)**, **SNS = pub/sub (push)**.

#### Serverless & additional compute — Module 3 (Exploring Compute Services) ✅ *(done — 29 Jun 2026)*
**Serverless** = run code without provisioning/managing servers; AWS handles provisioning, scaling, patching, availability. Wins: no server mgmt, auto-scaling, **pay only when running**, built-in HA.
**Compute spectrum (most control → least mgmt):** EC2 → Containers on EC2 (ECS/EKS) → Fargate/Lambda (serverless).

- **AWS Lambda** — event-driven (S3/API Gateway/SQS/schedule triggers); pay per request + ms duration, **$0 when idle**; auto-scales; **15-min max** per run → short tasks only.
- **Containers** — app + dependencies packaged (Docker); share host OS kernel → lighter/faster than VMs. **Orchestration** = managing many at scale. **ECS** (AWS-native) · **EKS** (managed Kubernetes) · **Fargate** (serverless — no EC2 hosts to manage) · **ECR** (image registry).
- **Additional compute:**
  - **Elastic Beanstalk** — PaaS; upload web app code → auto provisioning/LB/scaling/health, you still see resources. Fast web-app deploy.
  - **Amazon Lightsail** — simplest, low bundled-price VPS for simple sites/small apps/learning.
  - **AWS Batch** — run large batch computing jobs.
  - **AWS Outposts** — AWS infrastructure on-premises (hybrid).

> **Pick-the-compute:** full OS control → EC2 · fast web app, AWS-managed scaling → Beanstalk · simple cheap site → Lightsail · orchestrate containers → ECS/EKS (+Fargate to skip servers) · short event-driven code → Lambda.

### Global Infrastructure — Module 4 (Going Global) ✅ *(done 29 Jun 2026)*
**Hierarchy:** **Region** (geographic area) → contains multiple **Availability Zones (AZs)** (clusters of data centers) → **Edge Locations** (many more, separate sites, for caching/CDN).

- **Regions** — isolated geographic areas; **data stays in a Region** unless you move it (key for compliance / data residency). **Choosing a Region — 4 factors:** ① **Compliance** (legal/data-governance) ② **Proximity/latency** (close to users) ③ **Service/feature availability** (not every service is in every Region) ④ **Pricing** (varies by Region).
- **Availability Zones (AZs)** — one+ discrete data centers with redundant power/networking; isolated from other AZs' failures but linked by low-latency fiber. **Best practice: deploy across ≥2 AZs → high availability / fault tolerance.**
- **Edge Locations** — many worldwide sites that cache content close to users; used by **Amazon CloudFront**, Route 53, Global Accelerator.
- **Amazon CloudFront** — **CDN**: caches content at edge locations near users → faster delivery, lower latency.
- **AWS Local Zones** — push compute/storage closer to users when no Region is near enough (latency-sensitive apps).
- **AWS Wavelength** — embed compute/storage in **5G** networks for ultra-low latency to mobile users.
- **AWS Outposts** — run AWS infrastructure in **your own data center** (hybrid; extends a Region on-prem).

> **Exam framing:** AZ = data center(s) → use **multi-AZ** for HA. **Region choice = compliance · latency · service availability · price.** **CloudFront + Edge locations = cache content near users.** Data residency/compliance → Region isolation.

### Networking — Skill Builder Module 5 ✅ *(done 30 Jun 2026)*

**Big head start:** [[Networking]] already covers VPC, public/private subnets, route tables, Internet Gateway, NAT Gateway, VPC peering, DNS mechanics, and load balancers. The genuinely *new, exam-critical* pieces are: the **VPC connectivity menu** (IGW vs VPN/VGW vs Direct Connect), the precise **Security Group vs NACL** distinction, **Route 53** as a service, and **Global Accelerator**.

**Amazon VPC** — your own isolated, private virtual network inside AWS. Define its IP range with a **CIDR block** (e.g. `10.0.0.0/16`). **Regional** (spans the AZs of one Region). Carved into **subnets** (each in **one AZ**): **public** (has a route to an Internet Gateway) and **private** (no direct internet route — databases/app servers).

#### How traffic gets in & out — the connectivity menu *(the #1 tested networking concept)*
| Path | What it is | Over the internet? | Use it for |
|---|---|---|---|
| **Internet Gateway (IGW)** | The VPC's door to the **public internet**; public subnets route `0.0.0.0/0` → IGW | Yes (public) | Public-facing apps, web servers, load balancers |
| **Virtual Private Gateway (VGW) + Site-to-Site VPN** | The AWS end of an **encrypted VPN tunnel** between on-prem and the VPC | Yes, but **encrypted** | Quick, cheap hybrid link |
| **AWS Direct Connect (DX)** | A **dedicated private physical fibre line** from your data center to AWS — **bypasses the public internet** | **No** (private) | Consistent low latency, high bandwidth, large/sensitive data, compliance |

> **Exam trap:** **VPN = encrypted tunnel over the *public* internet** (fast to set up, cheap). **Direct Connect = your own *private* physical cable** (consistent, high-throughput, more expensive, weeks to provision). Both link **on-prem ↔ AWS**. **IGW** is for *public* internet traffic into the VPC.
> Memory hook: **IGW = public door · VPN = encrypted tunnel over the internet · Direct Connect = private dedicated cable, no internet.**
> 🔐 Full VPN mechanics (tunneling/encapsulation, IPsec, IKE phases, ESP, AWS CGW/VGW, two-tunnel HA): [[VPN]].

Also recognize by name (common distractors): **Transit Gateway** = hub-and-spoke router connecting many VPCs + on-prem in one place; **VPC Endpoints / PrivateLink** = reach AWS services privately without going over the internet.

#### Securing the VPC — Security Groups vs Network ACLs *(heavily tested)*
Packet path inward: **internet → IGW → subnet's NACL (border guard) → instance's Security Group (bouncer) → EC2.**

| | **Security Group** | **Network ACL (NACL)** |
|---|---|---|
| Operates at | **Instance** level (the ENI) | **Subnet** level |
| State | **Stateful** — return traffic auto-allowed | **Stateless** — must allow return traffic explicitly |
| Rule types | **Allow only** (everything else implicitly denied) | **Allow *and* Deny** |
| Evaluation | All rules evaluated together | Rules checked in **number order — first match wins** |
| Default | Denies all inbound, allows all outbound | *Default* NACL allows all; *custom* NACL denies all until you add rules |

> **Exam framing:** **Stateful = Security Group** (you only think about one direction; the reply is automatically allowed). **Stateless = NACL** (must allow inbound *and* the outbound return on ephemeral ports). Need to **explicitly DENY/block a specific IP?** → **NACL** (SGs can't deny). SG is the default instance firewall; NACL is an optional extra subnet-wide layer.
> Memory hook: **S**ecurity Group = **S**tateful · NA**C**L = **C**an say no (deny) + has no memory (stateless).

#### Amazon Route 53 — AWS's DNS
- Highly available, scalable **DNS** web service: names → IPs (the "phonebook" from [[Networking]] §7, as a managed AWS service).
- Also a **domain registrar** — register/buy domain names directly.
- Routes users to AWS resources (**ELB, CloudFront, S3 static sites**) and on-prem endpoints; integrates with **health checks**.
- **Routing policies** (know they exist + the headline ones):
  - **Simple** — one record, one resource.
  - **Weighted** — split traffic by % across endpoints (A/B testing, canary).
  - **Latency-based** — send users to the Region with the **lowest latency**.
  - **Geolocation** — route by the **user's physical location**.
  - **Geoproximity** — route by distance between user and resources.
  - **Failover** — send to a **backup** if the primary fails (disaster recovery).
  - **Multivalue answer** — return several healthy IPs.
- Classic combo: **Route 53 + CloudFront** for fast, global, highly available delivery.

#### Edge / global delivery
- **Amazon CloudFront** (Module 4 ✅) — **CDN**; **caches** content at **edge locations** near users → low latency; absorbs spikes & adds DDoS protection (with AWS Shield). HTTP/HTTPS content.
- **AWS Global Accelerator** — improves availability/performance by routing traffic over the **AWS global backbone** to the nearest edge, then to your app. Gives **static anycast IPs** + fast failover. **Does *not* cache.**

> **CloudFront vs Global Accelerator (exam trap):** **CloudFront = caches content** at the edge (static + dynamic web content, HTTP/HTTPS). **Global Accelerator = no caching** — it speeds up and adds static IPs for **TCP/UDP** apps (gaming, IoT, VoIP, APIs) by routing over AWS's private backbone, not the public internet.

> **Module 5 exam-day recap:** VPC = isolated network (CIDR, regional) → subnets (one AZ each; public has IGW route). **Into the VPC:** IGW (public) · VPN over VGW (encrypted, public internet) · Direct Connect (private dedicated line). **Firewalls:** Security Group = stateful, allow-only, instance level · NACL = stateless, allow+deny, subnet level. **Route 53 = DNS + registrar + routing policies. CloudFront = caches at edge; Global Accelerator = routes over backbone, no cache.**

### Storage — Skill Builder Module 6 ◐ *(in progress — 30 Jun 2026)*

**Master key — there are only 3 types of storage; every service maps to one.** *(Don't memorize 12 services — learn 3 ideas.)*

| Type | What it really is | Analogy | AWS service |
|---|---|---|---|
| **Block** | Raw disk cut into blocks; OS puts a filesystem on top; attaches to **one** machine | A hard drive/SSD in **one** computer | **Amazon EBS** |
| **File** | Files in folders over a network protocol (NFS/SMB); **many** machines mount at once | A shared **team network drive** | **Amazon EFS** (Linux/NFS), **Amazon FSx** (Windows/specialized) |
| **Object** | Whole objects (data + metadata + ID) in a flat pool, via **URL/API**; infinite scale | A **valet locker** — hand over the object, get a URL ticket | **Amazon S3** |

> **The one-liner:** **EBS = a disk for one server · EFS/FSx = a shared drive for many · S3 = a web locker for anything.**

#### EBS vs EFS — the classic trick question
| | **EBS** (block) | **EFS** (file) |
|---|---|---|
| Attaches to | **One** EC2 instance | **Many** EC2s at once |
| Scope | **One AZ** | **Regional** (spans AZs) |
| Sizing | You pick the size | **Auto-scales** elastically |
| Model | The instance's hard drive | A shared NFS drive |

> Hook: **E*B*S = one *B*ox · E*F*S = *F*leet (shared by many).** (EBS also: persists independently of the instance; **snapshots** are point-in-time backups stored in S3. *Instance store* = ephemeral, lost on stop — don't confuse with EBS.)

#### Amazon S3 — the heavy hitter (most-tested service on the exam)
Object storage: **unlimited**, **11 9's durability**, reached by **URL/API**, auto-stored across **multiple AZs** in a Region. Uses: backups, static websites, data lakes, media, app assets.

> 🪣 **Want the *why* behind every storage class** (the cost-dial model, durability-vs-availability, the 3 classic confusions): [[S3]] deep-dive.

**Storage classes — picture a kitchen** (don't rote-learn the list):
| Class | Kitchen analogy | When |
|---|---|---|
| **S3 Standard** | Food on the **counter** | Frequent access, default |
| **S3 Intelligent-Tiering** | **Smart fridge** that moves food for you | Access pattern unknown/changing — set & forget |
| **S3 Standard-IA** | The **pantry** | Rare access, instant when needed (retrieval fee) |
| **S3 One Zone-IA** | Pantry in **one room only** | Same, but lives in 1 AZ (cheaper, reproducible data) |
| **S3 Glacier Instant Retrieval** | **Freezer**, instant grab | Archive needed in milliseconds |
| **S3 Glacier Flexible Retrieval** | **Freezer** (thaw minutes–hours) | Archive, can wait a bit |
| **S3 Glacier Deep Archive** | **Deep freezer in the basement** | Cheapest, retrieve in hours; compliance/long-term |

> Pattern: **counter → pantry → freezer = more access ÷ less cost.** Less access + slower retrieval = cheaper.
> **Lifecycle policy** = rules that auto-move objects over time (Standard → IA → Glacier → delete). Exam cue: *"automatically move old data to cheaper storage"* → **lifecycle policy**.

**Exam trigger words → class** (learn the triggers, not the list — the two starred ones trip people up most):
| Question says... | Class |
|---|---|
| "frequently accessed" / default | **S3 Standard** |
| ⭐ **"unknown / changing / unpredictable"** access + **"automatic"** cost optimization | **S3 Intelligent-Tiering** |
| ⭐ **"infrequently accessed"** but **"available immediately / rapid"** | **S3 Standard-IA** |
| infrequent **+ "can tolerate"** single-AZ loss / "reproducible" / non-critical | **S3 One Zone-IA** |
| **"archive" / "long-term" / "rarely"** + retrieval-time tolerance | **S3 Glacier** (ms→Instant · min–hrs→Flexible · hrs + cheapest + compliance→Deep Archive) |

#### Moving big data — hybrid + transfer cluster
- **AWS Storage Gateway** — bridges **on-prem** apps to AWS storage (hybrid); local access continues while data backs to AWS. A gateway appliance (VM/hardware) on-prem **caches hot data locally** for low latency + syncs to AWS in the background, so apps keep their normal protocols and don't know the data went to the cloud.
  - **Pick the type by the interface your on-prem app speaks** (maps back to the 3 storage types): **S3 File Gateway** (NFS/SMB → objects in **S3**) · **FSx File Gateway** (SMB → **Amazon FSx for Windows**) · **Tape Gateway** (backup software / VTL → **S3 + Glacier/Deep Archive**, replaces physical tape) · **Volume Gateway** (iSCSI block → **S3 + EBS snapshots**). Families = **File / Tape / Volume**.
  - **Volume Gateway modes:** **Cached** = primary data in AWS, only hot data cached on-prem · **Stored** = entire dataset on-prem, async backups to AWS as EBS snapshots. Hook: *Cached = primary in cloud · Stored = primary on-prem, cloud is backup.*
  - **Exam-level takeaway:** trigger = *"keep using the on-prem app but store/back up data in AWS"* → **Storage Gateway**. The 4 types + 2 modes are nice-to-know, not heavily tested — don't over-study them.
- **AWS Backup** — one central place to back up across many AWS services.
- **AWS Snow Family** — physically **ship** data when the network is too slow: **Snowcone** (smallest, portable) → **Snowball Edge** (suitcase, TBs–PBs, + compute) → **Snowmobile** (a literal truck, exabytes). Hook: **cone < ball < mobile = small < medium < gigantic.**

> **Module 6 on one screen:** 3 types — EBS (disk for one server) · EFS/FSx (shared drive for many) · S3 (web locker). EBS vs EFS = one box vs a fleet. S3 classes = counter→pantry→freezer (access ÷ cost); **lifecycle** auto-moves them. **Snow** ships data physically (cone < ball < mobile).

<!-- Still to cover (Modules 7–8, 10): Databases (RDS, Aurora, DynamoDB, Redshift, ElastiCache), AI/ML & analytics, Mgmt/monitoring (CloudWatch, CloudTrail, CloudFormation, Trusted Advisor). Ways to access: Console, CLI, SDK, IaC. -->

## Domain 4 — Billing, Pricing & Support (12%)
<!-- Day 11. Pricing models (On-Demand, Reserved, Spot, Savings Plans, Dedicated). Free Tier (always-free / 12-month / trials). Cost tools: Cost Explorer, Budgets, Cost & Usage Report, Pricing Calculator. Organizations + consolidated billing. Support plans (Basic/Developer/Business/Enterprise) + Trusted Advisor checks. -->

---

## 📎 Resources (curated)

**🥇 Practice exams — the #1 thing for passing (drill to 80%+ before booking):**
- **Tutorials Dojo (Jon Bonso)** practice exams — *the* gold standard for AWS certs. Realistic difficulty + excellent explanations. Udemy / tutorialsdojo.com. **Buy this even if nothing else (~$15).**
- AWS Skill Builder **official practice exam** (free) — final confidence check.

**📚 Main course — pick ONE (reinforces Claude's teaching):**
- **Stephane Maarek** "Ultimate AWS CCP CLF-C02" (Udemy, ~$15) — most popular, polished, exam-focused.
- **Adrian Cantrill** Cloud Practitioner (cantrill.io) — **free**, deeper "why."
- **Andrew Brown / ExamPro** full CCP course (freeCodeCamp YouTube) — **free**, one ~13h video.

**🆓 Official AWS (free — do regardless):**
- **AWS Skill Builder** → "AWS Cloud Practitioner Essentials" course + official practice question set.
- **Official Exam Guide + sample questions** (AWS Certification page) — exactly what's tested.
- Whitepapers: "Overview of AWS", "AWS Well-Architected Framework", "How AWS Pricing Works".

**📝 Final-week review:**
- **Tutorials Dojo cheat sheets** (free) — concise per-service summaries. Great for Days 13–15.

> **My stack for this 2–3 wk intensive:** Claude + these notes (primary) → one free course (ExamPro/Cantrill) for reinforcement → **Tutorials Dojo practice exams** (Days 13–15, make-or-break) → AWS official practice exam (final check). Can be done 100% free, but Tutorials Dojo practice exams are the highest-ROI paid item.

---

## Source
Mapped to the **CLF-C02** exam guide (4 domains). Part of the broader DevOps journey — overlaps UDAAN Week 10 (Cloud). Full curriculum: [[Syllabus]].
