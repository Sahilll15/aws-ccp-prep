# Module 9 — Security

**Status: ⬜ upcoming** · Domain 2 (Security & Compliance — 30%, the heaviest domain) · We'll deepen this and build a visual page when we study it.

## Shared Responsibility Model
- **AWS = security OF the cloud** (hardware, global infrastructure, managed-service internals).
- **Customer = security IN the cloud** (your data, IAM config, OS patching on EC2, firewall rules).
- The line **shifts by service** (more managed = AWS handles more; e.g. Lambda vs EC2).

## IAM (Identity & Access Management)
- **Users, Groups, Roles, Policies** — *who* can do *what*. Policies = JSON permissions.
- **Roles** = temporary credentials for services/federation (preferred over long-lived keys).
- **MFA** — extra factor; enable on the **root user**.
- **Root user** — don't use for daily work; lock it down with MFA.
- **Principle of least privilege** — grant only what's needed.
- **IAM Identity Center** — single sign-on across accounts.

## Protective services
- **AWS Shield** — **DDoS** protection (Standard free, Advanced paid).
- **AWS WAF** — web application firewall (**Layer 7**, filters HTTP — SQLi/XSS).
- **Amazon GuardDuty** — intelligent **threat detection** (analyzes logs).
- **Amazon Inspector** — automated **vulnerability** assessments (EC2, containers).
- **Amazon Macie** — discovers/protects **sensitive data (PII) in S3**.
- **AWS KMS** — manage **encryption keys**. **Secrets Manager** — store secrets/rotate.
- **Amazon Cognito** — user sign-up/sign-in for apps.
- **Encryption**: in transit (TLS) vs at rest (KMS).

## Governance / compliance
- **AWS Organizations** + **SCPs** (Service Control Policies) — central multi-account guardrails.
- **AWS Artifact** — on-demand **compliance reports** (SOC, ISO, PCI).

## Likely exam framing
- DDoS → Shield · web exploits (L7) → WAF · threat detection → GuardDuty · vuln scan → Inspector · PII in S3 → Macie · encryption keys → KMS · compliance docs → Artifact · multi-account guardrails → Organizations/SCPs.
