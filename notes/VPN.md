# 🔐 How a VPN Actually Works

Deep-dive reference on Virtual Private Networks — the real mechanics (tunneling, IPsec, IKE, crypto), not just "it's a secure tunnel." Builds on [[Networking]] (encapsulation §4, TLS handshake §2, NAT §7, IPsec-at-L3). Tied to AWS **Site-to-Site VPN** / **Client VPN** for [[AWS-Cloud-Practitioner]] Domain 3.

← back to [[Networking]] · [[DevOps]] · [[AWS-Cloud-Practitioner]]

---

## The core idea

A **VPN (Virtual Private Network)** makes two endpoints behave as if they're on the same private LAN, even though traffic between them crosses the **public, untrusted internet**. Three pillars:

1. **Tunneling (encapsulation)** — wrap each packet inside another so private addressing is hidden and the internet routes it between two public endpoints.
2. **Encryption** — scramble the payload so a sniffer sees gibberish.
3. **Authentication + integrity** — each end proves its identity (no tunneling to an imposter) and every packet is integrity-checked (no tampering in flight).

> **One-liner:** a VPN is an encrypted, authenticated tunnel that carries private network traffic across a public network as if it were local.

## Two types

| | **Remote-access** (client-to-site) | **Site-to-site** |
|---|---|---|
| Connects | One **device** → a private network | Two whole **networks** |
| Examples | Corporate "connect to office", consumer privacy VPNs, **AWS Client VPN** | On-prem ↔ AWS VPC, office ↔ office, **AWS Site-to-Site VPN** |
| Your-side endpoint | VPN **client software** on the device | A VPN **gateway/router** (no per-device software) |
| Typical tech | TLS-based (OpenVPN), WireGuard, IKEv2 | **IPsec** |

The AWS exam's "VPN" (the VGW one) is **site-to-site**.

## Pillar 1 — Tunneling / encapsulation

A VPN does an *extra* wrap beyond normal encapsulation ([[Networking]] §4): it puts a whole finished IP packet inside the payload of a new packet.

```
Original packet (inside the private network):
  [IP: 10.0.1.5 → 192.168.2.8][TCP][data]

After IPsec tunnel-mode encapsulation:
  [IP: 198.51.100.7 → 203.0.113.20]   ← new OUTER header (the two gateways' PUBLIC IPs)
     [ESP header]
        [ ENCRYPTED { [IP:10.0.1.5 → 192.168.2.8][TCP][data] } ]  ← whole original packet, encrypted
     [ESP auth/trailer]
```

The internet sees only the **outer** header (public IP A → public IP B). Private addressing + data are encrypted inside and invisible. That's the "virtual private" part.

## Pillars 2 & 3 — encryption + authentication (same pattern as TLS)

Mirrors the TLS handshake ([[Networking]] §2): asymmetric crypto to bootstrap, symmetric to do bulk work.

- **Diffie-Hellman key exchange** — both ends derive a **shared secret over the public internet without ever sending it**. An eavesdropper seeing the public values can't compute it.
- **Symmetric encryption (AES, ChaCha20)** — fast bulk encryption of the traffic, using keys from that exchange.
- **Hashing / HMAC (SHA-256)** — integrity; proves the packet wasn't altered.
- **Perfect Forward Secrecy (PFS)** — fresh DH keys per session, so compromising one session never exposes past ones.

## Protocol landscape

| Protocol | Layer | Used for | Notes |
|---|---|---|---|
| **IPsec** | L3 | Site-to-site (+ IKEv2 remote-access) | The classic. What **AWS Site-to-Site VPN** uses. |
| **TLS/SSL VPN** (OpenVPN, AnyConnect) | rides TLS | Remote-access | Often on **port 443** to pass firewalls. **AWS Client VPN** is OpenVPN-based. |
| **WireGuard** | L3 (UDP) | Modern everything | Tiny codebase, fixed modern crypto (ChaCha20 / Curve25519), roaming-friendly, "cryptokey routing" (peer = its public key). |
| **PPTP / L2TP / SSTP** | various | Legacy | PPTP broken/dead; L2TP usually L2TP/IPsec. |

## IPsec deep dive (what AWS uses)

A suite with two jobs: **negotiate keys (IKE)**, then **protect data (ESP/AH)**.

### IKE (Internet Key Exchange) — the handshake, two phases
- **Phase 1 — secure management channel.** Gateways authenticate (pre-shared key or certificates) + run Diffie-Hellman → establish the **IKE SA**. Runs on **UDP 500**.
- **Phase 2 — the data tunnel.** Inside the Phase-1 channel, negotiate cipher/keys/which-traffic → create the **IPsec SAs**. This is the tunnel data rides in.
- **IKEv2** = modern (fewer round trips, better re-keying, survives network changes via MOBIKE). IKEv1 = older but common.

### ESP vs AH
- **ESP (Encapsulating Security Payload)** — **encrypts AND authenticates** the payload. The one actually used. IP protocol **50**.
- **AH (Authentication Header)** — integrity only, **no encryption**, **breaks through NAT**. Protocol 51. Rare.

### Transport vs tunnel mode
- **Transport** — encrypts payload only, keeps original IP header (host-to-host).
- **Tunnel** — encrypts the **entire original packet** + new IP header. **Site-to-site uses this.**

### Security Association (SA)
A **one-way** agreement (cipher + keys + rules for one direction). A working tunnel needs **two SAs** (one each way). Identified by an **SPI (Security Parameter Index)** in the ESP header so the receiver picks the right keys.

### NAT traversal (NAT-T)
Plain ESP has no ports → breaks crossing a NAT ([[Networking]] §7). **NAT-T** wraps ESP in **UDP 4500** so the NAT has a port to track. Needed because nearly every on-prem router is behind NAT (AWS handles it).

## End-to-end: a packet through a site-to-site VPN
1. Host A (`10.0.1.5`) → Host B (`192.168.2.8`) on the remote net.
2. A's routing: "`192.168.2.0/24` → VPN gateway" → packet goes to **Gateway A**.
3. Gateway A matches IPsec policy → **encrypts** the whole packet (ESP) + **wraps** it `[GW-A public IP → GW-B public IP]`.
4. Crosses the internet — sniffers see only an encrypted blob between two public IPs.
5. **Gateway B** authenticates (integrity check), **decrypts**, recovers the original packet.
6. Gateway B forwards it onto its LAN to Host B.
7. Return traffic = exact reverse (other SA).

## Remote-access mechanics (laptop / consumer VPN)
- Client creates a **virtual interface**: **TUN** (L3/IP packets) or **TAP** (L2/Ethernet frames); OS treats it as a real NIC.
- After auth, the server assigns a **virtual IP** from the private range.
- The OS **routing table is rewritten** so target traffic enters the virtual interface → client encrypts → sends over a normal socket to the VPN server → server decrypts + injects into the network.
- **Split tunnel** = only private-network traffic via VPN; **full tunnel** = *all* traffic via VPN.
- **Why consumer privacy VPNs hide your IP:** full-tunnel → all traffic exits from the **VPN server's IP**; sites see that, not you; ISP sees only encrypted traffic to the server. Catch: **trust shifts entirely to the VPN provider**.

### Geo-unblocking — "watch another country's content"
Same machinery, one twist: **pick a full-tunnel exit server in country X**, and your traffic reaches the internet from *that country's* IP.
- **Why it works = IP geolocation.** Your public IP must be real/routable (it's the return address). IP blocks are allocated by region; commercial DBs (e.g. **MaxMind**) map `IP range → country`. Sites just look up your **exit IP**. No VPN → ISP's India IP (you look Indian). VPN→US server → server's US IP (you look American). You don't hide your location, you **borrow** the exit node's.
- **Flow:** You (India) → encrypted full tunnel → **VPN server (USA)** makes the request from its US IP → Netflix sees a US IP → serves the US catalog → response back through the tunnel.
- **DNS must go through the tunnel too** — else a query to your real ISP resolver = a **DNS leak** that exposes your true location. VPN pushes its own resolvers.
- **Why it breaks:** streaming services run **VPN detection** — blocklists of known datacenter/VPN IP ranges → *"you appear to be using a proxy/unblocker."* Providers counter with rotating + residential IPs. Permanent cat-and-mouse (same server works one week, not the next).
- Contrast: this is **full tunnel + remote-access** (disguise location); a typical corporate OpenVPN is **split tunnel** (reach private resources, only some traffic in). Opposite goals, same tech.

## AWS angle (exam-relevant)
**AWS Site-to-Site VPN** = textbook IPsec tunnel mode:
- **Customer Gateway (CGW)** = resource describing **your** side (on-prem router public IP, BGP ASN).
- **Virtual Private Gateway (VGW)** = the **AWS** side, attached to the VPC (or attach to a **Transit Gateway** for many VPCs).
- AWS provisions **two tunnels** to two endpoints for **HA/redundancy**.
- Routing **static or dynamic (BGP)**; IPsec (IKE + ESP), **encrypted, over the public internet**.

**AWS Client VPN** = managed **remote-access** flavor (OpenVPN/TLS) for individual users reaching the VPC.

> **Exam nuance:** **Direct Connect alone is private but NOT encrypted** (dedicated physical line, no tunnel). Need dedicated line *and* encryption → run a **VPN over Direct Connect**. Common distractor. See [[AWS-Cloud-Practitioner]] Domain 3 connectivity menu.

## Worked example — corporate OpenVPN (remote-access), and a common confusion

**OpenVPN is remote-access + TLS-based — it has NO Virtual Private Gateway.** VGW is an AWS **site-to-site IPsec** construct (two *networks*); a person on a laptop logging in is **remote-access**. The box that feels like a "gateway" in an OpenVPN setup is just the **OpenVPN server / concentrator** (typically an instance/appliance inside the company's AWS VPC).

| | **OpenVPN** (typical corporate) | **AWS Site-to-Site VPN (VGW)** |
|---|---|---|
| Type | Remote-access (a person) | Site-to-site (two networks) |
| Tech | **TLS/SSL** (OpenSSL certs) | **IPsec** (IKE + ESP) |
| Your side | OpenVPN **client app** | A router/gateway |
| Concentrator | An **OpenVPN server** | A **Virtual Private Gateway** |

**Corrected step-by-step flow:**
1. **Auth happens ONCE at tunnel setup** — mutual TLS: server cert + **client cert** (+ usually username/password, often MFA). Not per-request.
2. Server assigns a **virtual IP** from the VPN pool (e.g. `10.8.0.6`), bound to a **TUN** interface on *your* laptop.
3. Server **pushes routes to *your* machine** ("corporate ranges → the tun interface"). The send-side routing lives on **your** box, not the destination server. (Split tunnel = only corp ranges; full = everything.)
4. You hit an internal app → OS matches a pushed route → packet into TUN → OpenVPN **encrypts** → ships to the OpenVPN server.
5. OpenVPN server **decrypts + forwards into the VPC/corp network**. Return routing to your virtual IP is handled by the **OpenVPN server** — either a route for the VPN pool points back at it, or it **NATs** your traffic to its own IP (so the app server never even knows your `10.8.0.6` exists).

> **The misconception to avoid:** the destination app server does **not** list your virtual IP in its routing table, and there is **no VGW** authenticating each request. Auth is one-time (mutual TLS); the OpenVPN server is the only component that knows your virtual IP and does the routing/NAT on both ends.

## VPN vs neighbors + gotchas
- **vs HTTPS/TLS:** HTTPS encrypts *one app's* connection; a VPN encrypts at the **network layer** for everything and hides routing/addresses.
- **vs proxy:** proxy = app-level, often unencrypted; VPN = OS-level, encrypted, all traffic.
- **Overhead:** crypto + extra header cost CPU and bytes; the header can push past the **MTU** → fragmentation → often **clamp the MSS**.
- **Not anonymity:** doesn't stop malware or make you untraceable; provider/employer can still see traffic. Gateway is a **bottleneck / SPOF** unless made redundant.

---

## Source
Taught in the AWS CLF-C02 study session, 2026-06-29, off the back of [[AWS-Cloud-Practitioner]] Module 5 (Networking). Mechanics-level companion to the exam-level VPN coverage in the hub's Domain 3.
