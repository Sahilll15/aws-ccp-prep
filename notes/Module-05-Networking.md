# Module 5 — Networking

**Status: ✅ done** · Domain 3 · Full notes: [Study hub](AWS-Cloud-Practitioner.html) → Networking · [VPN deep dive](VPN.html) · visual page [Networking & Storage](../networking-and-storage.html).

## Key points
- **Amazon VPC** — isolated private network (CIDR like `10.0.0.0/16`, **regional**). Subnets live in **one AZ each**: public (IGW route) / private (no direct internet).
- **Connectivity menu** (most-tested): **IGW** = public internet door · **Site-to-Site VPN** (Virtual Private Gateway) = encrypted tunnel over the internet · **Direct Connect** = private dedicated physical line, bypasses internet (not encrypted alone).
- **Security Group vs NACL**: SG = **stateful**, instance level, allow-only · NACL = **stateless**, subnet level, allow **and** deny. Block a specific IP → **NACL**.
- **Route 53** — DNS + domain registrar; routing policies (simple/weighted/latency/geolocation/failover).
- **CloudFront vs Global Accelerator**: CloudFront **caches** at edge (HTTP) · Global Accelerator **no cache**, routes TCP/UDP over AWS backbone + static IPs.

> Hooks: IGW=public door · VPN=encrypted tunnel · Direct Connect=private cable. SG=Stateful · NACL=can say No (deny).
