# Awesome-Object-Storage

## Top Object Storage Tools Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on S3 Compatibility, Erasure Coding & Self-Hosted Data Sovereignty*  
**Last updated: March 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Object Storage**. These tools store and retrieve unstructured data as objects — images, videos, backups, logs, and AI training datasets — using a flat namespace and HTTP APIs, typically S3-compatible, that scale from gigabytes to petabytes without a traditional filesystem hierarchy.

**Examples** include Amazon S3, Google Cloud Storage, Azure Blob Storage, Cloudflare R2, Backblaze B2, MinIO, Ceph RADOS Gateway, SeaweedFS, Garage, and Apache Ozone (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, S3 API compatibility, and transparent data placement — especially critical now that **MinIO's Community Edition entered maintenance mode in December 2025**, leaving a vacuum in the "default open-source S3 engine" slot [citation:1].

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **Amazon S3** — The reference object storage service and de facto S3 API standard. Virtually unlimited scale with lifecycle policies, versioning, and storage classes from hot to Glacier. **Best for AWS-native workloads** needing the broadest ecosystem compatibility.

- **Google Cloud Storage** — GCP's object store with strong consistency, multi-region buckets, and integration with BigQuery and Vertex AI.

- **Azure Blob Storage** — Microsoft's object storage with hot/cool/archive tiers and deep integration with Azure services.

- **Cloudflare R2** — S3-compatible storage with **zero egress fees**, making it attractive for multi-cloud and CDN-adjacent workloads.

- **Backblaze B2** — Low-cost S3-compatible storage with free egress up to 3x average monthly storage.

- **Wasabi** — Hot storage with no egress fees and predictable per-TB pricing.

## Open-Source GitHub Projects

- **[Ceph RADOS Gateway (radosgw)](https://github.com/ceph/ceph)**  
  **The enterprise-grade S3/Swift gateway backed by Ceph's distributed object store** — LGPL-2.1 licensed . **Provides a REST gateway implementing a superset of Amazon S3 and OpenStack Swift APIs** over RADOS, Ceph's distributed object store [citation:3][citation:11]. **Battle-tested at petabyte scale** in OpenStack and enterprise deployments. **Trade-offs**: **operational complexity is high** — requires a full Ceph cluster (MON, OSD, MGR, MDS) and careful tuning. **Best for organizations already running Ceph** or needing unified block/file/object storage from one platform.

- **[SeaweedFS](https://github.com/seaweedfs/seaweedfs)**  
  **The high-performance distributed object store with O(1) disk reads** — Apache 2.0 licensed . **Every file resolves to a single disk seek**, keeping read latency flat and sub-millisecond whether you store millions or billions of files . **Append-only writes** mean data is immutable and recoverable by design, with sequential I/O keeping ingestion fast . **Serves S3 objects, POSIX files, HDFS jobs, and Iceberg tables from the same cluster and the same copy of data** — no gateways or sync jobs between systems [citation:12]. **Enterprise adds** customizable erasure coding (e.g., 20+4 = 1.2× overhead), zstd compression, data recovery/undelete, point-in-time recovery, self-healing storage, and OIDC admin UI [citation:12]. **Open-source edition includes** S3/FUSE/HDFS/Iceberg APIs and fixed-ratio erasure coding . **Best for teams wanting a single cluster serving object, file, and lakehouse workloads** with predictable performance at scale.

- **[Garage](https://github.com/deuxfleurs-org/garage)**  
  **The lightweight, geo-distributed S3 store for small-to-medium self-hosting** — AGPLv3 licensed . **Designed for clusters composed of nodes at different physical locations**, replicating data across sites and staying available when some servers are unreachable [citation:5]. **Focuses on being lightweight, easy to operate, and highly resilient to machine failures** — built by Deuxfleurs, a small self-hosted service provider using it in production since 2020 [citation:5]. **The community's leading candidate to replace MinIO for small-scale deployments** [citation:1]. **Trade-offs**: designed for small-to-medium scale, not petabyte-class enterprise workloads. **Best for homelabs, small teams, and geo-distributed edge deployments** wanting simple, resilient S3-compatible storage.

- **[Apache Ozone](https://github.com/apache/ozone)**  
  **The cloud-native distributed object store for big data and AI** — Apache 2.0 licensed, ASF-governed . **Ozone 2.0.0** is the first object store to **support Apache HBase**, enabling low-latency read/write operational workloads alongside traditional object storage [citation:6]. **Atomic key operations** for concurrent consistency, modernized Recon monitoring UI, JDK 17/21 and native ARM64 support, and improved snapshots for large-scale environments [citation:6]. **S3 gateway** with lifecycle configurations, STS temporary credentials, and Trino integration on the roadmap [citation:14]. **Best for Hadoop-ecosystem organizations** needing an object store that also handles operational database workloads, backed by Apache governance rather than a single vendor.

- **[OpenStack Swift](https://github.com/openstack/swift)**  
  **The original open-source object store, battle-tested at scale** — Apache 2.0 licensed . **Creates redundant, scalable object storage using clusters of standardized servers to store petabytes of accessible data** [citation:7]. **No central "brain" or master point of control** — greater scalability, redundancy, and permanence [citation:7]. **Objects are written to multiple hardware devices**, with software ensuring replication and integrity across the cluster. **Can use inexpensive commodity hard drives and servers** in lieu of expensive equipment [citation:7]. **Best for OpenStack deployments** and organizations already invested in the OpenStack ecosystem.

- **[Kypello](https://github.com/kypello-io/kypello)**  
  **The community-maintained MinIO fork preserving OIDC/SSO and full Admin UI** — AGPLv3 licensed . **Forked specifically to restore enterprise identity features removed from upstream MinIO**: **OpenID Connect (OIDC), SSO, and the comprehensive Admin UI** [citation:2]. **S3 API compatible** with existing tools and SDKs, **built-in support for Keycloak, Okta, Active Directory, and Google Workspace** [citation:2]. **Full web console** for managing buckets, users, and groups. **Legal note**: based on MinIO's open-source code but not affiliated with or endorsed by MinIO Inc. [citation:2]. **Trade-offs**: young project with no commercial license exception — all usage must comply with AGPLv3 [citation:2]. **Best for MinIO users** who need OIDC/SSO and a full UI without migrating to MinIO Enterprise.

- **[Zenko CloudServer](https://github.com/scality/cloudserver)**  
  **Scality's open-source S3-compatible server** — Apache 2.0 licensed . **Written in Node.js and deployable in a Docker container** — from start to deployment complete in minutes [citation:8]. **Full AWS S3 API compatibility** with language-specific SDKs and wrappers, enabling ready-to-run S3 applications for backup, archiving, and collaboration [citation:8]. **Originally released as Scality S3 Server in June 2016**, renamed CloudServer and positioned as the core of Zenko's multi-cloud data controller [citation:8]. **Best for developers** wanting a quick S3-compatible server for local development or on-premises application testing.

### Additional Strong Open-Source Options

- **MinIO (Community Edition)** — **In maintenance mode since December 2025** — no new features, security fixes evaluated case-by-case [citation:1]. Still functional for existing deployments, but **do not start new projects on it** unless you plan to migrate to Enterprise or a fork like Kypello .
- **RustFS** — Rust-based S3-compatible object storage positioned as a MinIO alternative. Apache 2.0 licensed. Emerging project with community momentum [citation:1].
- **Apache Ozone S3 Gateway** — The S3-compatible interface to Ozone, supporting lifecycle and STS credentials [citation:14].

**Frameworks for building custom systems**: Combine **SeaweedFS** for a single cluster serving S3 objects, POSIX files, and Iceberg tables with predictable O(1) reads, **Garage** for lightweight geo-distributed small-to-medium deployments, **Ceph RADOS Gateway** for enterprise-grade S3/Swift backed by a full storage platform, **Apache Ozone** for Hadoop-adjacent workloads needing HBase support, and **Kypello** as a MinIO migration path preserving OIDC/SSO — to build an object storage layer tailored to your scale, governance requirements, and operational appetite.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- Object storage tools differ significantly in scale ceiling, operational complexity, and governance model. **MinIO's Community Edition entered maintenance mode in December 2025** — no new features, security fixes evaluated case-by-case, and the company encourages migration to MinIO Enterprise [citation:1]. **Projects hosted by foundations (Apache, OpenStack, CNCF) are immune to single-vendor rug-pulls** — SeaweedFS, Garage, and Ozone have different governance risks than single-vendor projects [citation:1]. **Ceph requires a full cluster** — RADOS Gateway is not a standalone binary. **Garage is designed for small-to-medium scale** — not petabyte-class enterprise workloads. **Kypello is a young fork** with AGPLv3-only licensing and no commercial exception [citation:2]. **S3 compatibility varies** — test your specific SDK operations against each implementation before committing.
- Self-hosted open-source solutions require proper erasure coding or replication configuration, disk failure monitoring, and awareness that "S3-compatible" does not mean "identical to S3 in every edge case."

---

**Made for platform engineers, data architects, and teams building object storage they can own and control.**
Let's make object storage more open, S3-compatible, and governance-transparent.
