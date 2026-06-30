# Module 4 — Going Global (Global Infrastructure)

**Status: ✅ done** · Domain 3 · Full notes in the [Study hub](AWS-Cloud-Practitioner.html) → Domain 3 Global Infrastructure.

## Key points
- **Hierarchy**: **Region** (geographic area) → **Availability Zones (AZs)** (1+ discrete data centers, isolated, low-latency linked) → **Edge Locations** (many more, for caching/CDN).
- **Regions** — isolated; **data stays in a Region** unless you move it (compliance/residency). **Choose a Region by 4 factors**: ① compliance ② proximity/latency ③ service availability ④ pricing.
- **AZs** — deploy across **≥2 AZs** → high availability / fault tolerance.
- **Amazon CloudFront** — CDN; caches content at edge locations near users.
- **AWS Local Zones** — compute/storage closer to users (latency-sensitive).
- **AWS Wavelength** — compute in **5G** networks (ultra-low latency to mobile).
- **AWS Outposts** — AWS infrastructure in **your** data center (hybrid).

> Exam: multi-AZ = HA · Region choice = compliance/latency/services/price · CloudFront+Edge = cache near users.
