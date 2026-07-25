# Virtualisation Basics — TryHackMe

- **Platform:** TryHackMe
- **Room:** Virtualisation Basics
- **Date Completed:** June 2026
- **Method:** YouTube walkthrough + notes
- **Medium Article:** N/A — conceptual room, GitHub notes only

---

## Why Virtualisation?

**Old thumb rule:** One server = one application

**Problem this caused:**
- Company needing website + database + email + internal app = 4 separate physical servers
- High cost, low utilisation, slow development, hard to scale

**Solution:** Multiple applications share the same physical server safely using a virtualisation layer.

---

## The Building Analogy

| Real World | Virtualisation |
|-----------|----------------|
| Building | Physical server |
| Apartments | Virtual Machines (VMs) |
| Tenants | Applications / Operating Systems |
| Building Manager | Hypervisor |

---

## Hypervisor — The Core of Virtualisation

Software that creates and manages Virtual Machines.

### Two Types:

| Type | Runs On | Best For | Examples |
|------|---------|----------|---------|
| **Type 1** (Bare Metal) | Directly on physical hardware | Servers, production | VMware ESXi, Hyper-V |
| **Type 2** (Hosted) | On top of existing OS | Learning, testing | VMware Workstation, VirtualBox |

---

## Virtual Machine (VM)

A complete virtual computer created by the hypervisor.
- Has own virtual CPU, RAM, storage, network
- Can run any OS
- Completely isolated — if one VM crashes, others keep working

### Security Use Case:
Testing malicious files — run them inside a VM. If it's malware, only the VM is affected, not your main machine. This is exactly how malware analysts do **dynamic analysis**.

---

## Containers — Lightweight Alternative to VMs

| Feature | VM | Container |
|---------|-----|-----------|
| Has own OS | Yes | No (shares host OS) |
| Startup time | Minutes | Seconds |
| Size | GBs | MBs |
| Use case | Full system isolation | Single app deployment |

**Docker** = most popular containerisation platform.

---

## Security Relevance

- Malware analysis → run malware safely in isolated VM
- Pen testing → run Kali Linux in VM on Windows machine
- TryHackMe → all vulnerable machines run in VMs/containers
- Docker misconfigurations = real attack vector (exposed Docker socket = root on host)
- VM escape attacks = attacker breaks out of VM to access host

---

## Key Takeaways
1. Virtualisation solves hardware inefficiency — one physical server, many virtual ones
2. Hypervisor manages VMs — Type 1 for production, Type 2 for learning
3. VMs = full isolated computers; Containers = lightweight isolated processes
4. Docker is the dominant containerisation platform
5. VMs are the foundation of all cybersecurity labs
6. Container misconfigurations are a real and growing attack surface
