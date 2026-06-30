# Module 6 — Storage

**Status: ✅ done** · Domain 3 · Full notes: [Study hub](AWS-Cloud-Practitioner.html) → Storage · [S3 deep dive](S3.html) · visual page [Networking & Storage](../networking-and-storage.html).

## Key points
- **3 storage types**: **Block** = EBS (disk for one EC2) · **File** = EFS/FSx (shared drive for many) · **Object** = S3 (web locker, infinite scale).
- **EBS vs EFS**: EBS = one instance, one AZ, you size it · EFS = many instances, regional, auto-scales. (EBS hook = one **B**ox · EFS = **F**leet.)
- **Amazon S3** — object storage, 11 nines durability, multi-AZ, accessed by URL/API. **Storage classes** = one cost dial (same durability; differ on cost / retrieval speed / availability):
  - Standard · Intelligent-Tiering (unknown pattern, auto) · Standard-IA (infrequent, instant) · One Zone-IA (recreatable, 1 AZ) · Glacier Instant/Flexible/Deep Archive (archive, ms→hours).
- **Lifecycle policy** = auto-move objects to cheaper classes over time.
- **Moving big data**: **Storage Gateway** (hybrid on-prem↔AWS) · **AWS Backup** · **Snow Family** (cone < ball < mobile = ship data physically).

> Triggers: unknown pattern → Intelligent-Tiering · recreatable/cheap → One Zone-IA · "auto move old data" → lifecycle policy.
