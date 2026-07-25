# Cloud Computing Basics — TryHackMe

- **Platform:** TryHackMe
- **Room:** Cloud Computing Basics
- **Date Completed:** June 2026
- **Method:** YouTube walkthrough + notes
- **Medium Article:** N/A — conceptual room, GitHub notes only

---

## What is Cloud?
Cloud is built on top of **virtualisation and containers** — the previous room's concepts directly apply here.

It allows you to run applications on **shared infrastructure** and quickly create/change environments when needed.

**Simple example:** Files on your laptop that you want to access from anywhere → Cloud solves this.

---

## Benefits of Cloud

| Benefit | Meaning |
|---------|---------|
| **Scalability** | Grow or shrink resources instantly based on demand |
| **On-demand self-service** | Provision resources yourself, no waiting for IT team |
| **Pay only for what you use** | No upfront hardware cost — usage-based billing |
| **Security** | Cloud providers invest heavily in security infrastructure |
| **High availability** | Built-in redundancy — services stay up even if one server fails |
| **Global access** | Access from anywhere in the world |

---

## Types of Cloud

| Type | Used By | Why |
|------|---------|-----|
| **Public** | Startups, websites, global apps | Cost effective, scalable, quick to set up |
| **Private** | Banks, healthcare, government | Control, customisation, compliance requirements |
| **Hybrid** | E-commerce companies | Balance of public scalability + private control |

---

## Cloud Service Models

| Model | Full Name | Who Manages What | You Handle |
|-------|-----------|-----------------|------------|
| **IaaS** | Infrastructure as a Service | Provider manages physical servers only | VMs, OS, apps, data |
| **PaaS** | Platform as a Service | Provider manages OS + infrastructure | Develop, deploy, run your app |
| **SaaS** | Software as a Service | Provider manages everything | Just use the software via browser |

**Real world examples:**
- IaaS → AWS EC2, Azure VMs (rent raw compute)
- PaaS → Heroku, Google App Engine (deploy code directly)
- SaaS → Gmail, Spotify, Netflix (just use the app)

---

## Major Cloud Vendors

- **AWS** (Amazon Web Services) — market leader
- **Microsoft Azure** — dominant in enterprise
- **Google Cloud Platform (GCP)**
- **Alibaba Cloud** — dominant in Asia
- **IBM Cloud**
- **Oracle Cloud**

---

## Real World Apps on Cloud
Netflix, Instagram, Spotify, online shopping apps — all rely on cloud infrastructure.

**EC2 (Elastic Compute Cloud)** = Amazon's cloud compute service — virtual machines you can create, use, and resize whenever needed.

---

## Security Relevance — Cloud Attack Surface

Cloud introduces new attack vectors that pen testers need to know:

| Attack Type | Description |
|-------------|-------------|
| **Misconfigured S3 buckets** | Public AWS storage buckets exposing sensitive data |
| **IAM misconfigurations** | Overly permissive roles allowing privilege escalation |
| **Exposed cloud metadata** | SSRF attacks accessing `169.254.169.254` to steal credentials |
| **Insecure APIs** | Cloud services exposed without proper authentication |
| **Container escape** | Breaking out of Docker container to host (cloud server) |

Cloud security is one of the **fastest growing** specialisations in cybersecurity right now.

---

## GATE CS Connection
- Cloud = distributed computing concepts → OS + CN overlap
- Virtualisation (previous room) is the foundation of cloud
- IaaS/PaaS/SaaS → standard questions in CS fundamentals

---

## Key Takeaways
1. Cloud is built on virtualisation and containers — same concepts, bigger scale
2. Three cloud types: Public (open), Private (controlled), Hybrid (both)
3. Three service models: IaaS (raw compute), PaaS (platform), SaaS (complete software)
4. AWS, Azure, GCP are the big three — AWS EC2 is the most referenced in security contexts
5. Cloud misconfigurations (S3 buckets, IAM roles) are among the most common real-world vulnerabilities
6. Cloud security is a high-growth specialisation — directly relevant to your career path
