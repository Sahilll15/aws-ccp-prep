# Moving & Managing Data with AWS

Module 6 deep dive. Three services that all "move data" but do **different jobs**. Visual page: [Moving Data to AWS](../moving-data-to-aws.html).

## 3 services, 3 jobs (anchor this)
| Service | Job | One-time / ongoing | How |
|---|---|---|---|
| **Storage Gateway** | On-prem apps use AWS as storage backend | Ongoing | Online (local cache) |
| **AWS Backup** | Scheduled, centralized backups + retention | Ongoing | Online (policy) |
| **Snow Family** | One-off bulk move of huge data | One-time | Offline (physical) |

> One line: **Storage Gateway = hybrid access · AWS Backup = scheduled backups · Snow = bulk migration by box/truck.**

## Storage Gateway (hybrid bridge)
Appliance on-prem presents the storage protocol your apps speak, caches hot data locally, syncs to AWS. Types by interface:
- **S3 File Gateway** (NFS/SMB → S3 objects) · **FSx File Gateway** (SMB → FSx Windows) · **Tape Gateway** (VTL → S3+Glacier, replaces physical tape) · **Volume Gateway** (iSCSI → S3+EBS snapshots).
- **Volume modes**: Cached (primary in AWS) vs Stored (primary on-prem, async backup to AWS).
- Trigger: "keep using on-prem app, store/back up in AWS" → Storage Gateway.

## AWS Backup (centralized backups)
One policy-driven place to automate backups across AWS services (vs per-service scripts).
- **Backup plan** — frequency + retention + lifecycle to cold storage.
- **Backup vault** — encrypted store of recovery points.
- **Cross-Region / cross-account** copies — for DR.
- **Vault Lock** — WORM immutability (ransomware/compliance protection).
- **Backup Audit Manager** — prove policy compliance.
- Covers EC2/EBS, RDS, Aurora, DynamoDB, EFS, FSx, S3, Storage Gateway, etc.
- Trigger: "centrally automate backups across services" / "retention + compliance" → AWS Backup (+ Vault Lock for immutable).

## Snow Family (ship it physically)
Rugged encrypted devices AWS ships → you load → ship back → imported to S3. Use when internet upload would take weeks+.
| Device | Capacity | Form | Use |
|---|---|---|---|
| **Snowcone** | ~8 TB HDD / 14 TB SSD | smallest, portable | small/edge transfers |
| **Snowball Edge** | ~80 TB (PB w/ many) | suitcase | TB–PB; compute-optimized has vCPU/GPU for edge |
| **Snowmobile** | up to 100 PB | 45-ft truck container | exabyte / data-center migration |
- **Edge compute**: run EC2/Lambda on Snowcone/Snowball **offline** in disconnected sites.
- Mnemonic: **cone < ball < mobile = small < medium < gigantic.**

## Exam triggers
- on-prem + AWS storage, hybrid, cache → **Storage Gateway** · replace tape → **Tape Gateway**
- centrally automate backups → **AWS Backup** · immutable/ransomware-proof → **Vault Lock**
- 50 TB slow internet → **Snowball** · portable/edge → **Snowcone** · whole data center / exabytes → **Snowmobile**
