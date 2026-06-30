# Module 7 — Databases

**Status: ⬜ upcoming (next)** · Domain 3 · We'll deepen this and build a visual page when we study it.

## Topic outline (starting reference)
- **Amazon RDS** — managed **relational** database (handles patching, backups, HA). Engines: MySQL, PostgreSQL, MariaDB, Oracle, SQL Server. **Multi-AZ** = standby copy for failover (HA); **Read Replicas** = scale reads.
- **Amazon Aurora** — AWS's own relational engine, **MySQL/PostgreSQL-compatible**, ~5x/3x faster, fully managed, auto-scaling storage. Pricier but high performance.
- **Amazon DynamoDB** — managed **NoSQL** key-value/document DB. **Serverless**, single-digit-millisecond latency, virtually unlimited scale. No schema.
- **Amazon Redshift** — **data warehouse** for analytics / OLAP (query petabytes with SQL). Think reporting, not transactions.
- **Amazon ElastiCache** — managed **in-memory** cache (**Redis** or **Memcached**) to speed up reads.
- **Amazon MemoryDB for Redis** — durable in-memory database.
- **DynamoDB Accelerator (DAX)** — in-memory cache **for DynamoDB** (microsecond reads).
- **Migration**: **DMS** (Database Migration Service — move DBs to AWS, minimal downtime) · **SCT** (Schema Conversion Tool — convert between engines).

## Likely exam framing
- "Managed **relational** DB" → **RDS**. "MySQL/Postgres-compatible, high performance" → **Aurora**.
- "**NoSQL**, key-value, serverless, millisecond scale" → **DynamoDB**.
- "**Data warehouse** / analytics / BI queries" → **Redshift**.
- "Speed up a database with **caching**" → **ElastiCache** (or **DAX** for DynamoDB).
- "Migrate a database to AWS" → **DMS** (+ **SCT** if changing engine).
