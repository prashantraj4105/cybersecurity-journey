# Computer Types — TryHackMe

- **Platform:** TryHackMe
- **Room:** Computer Types
- **Date Completed:** June 19, 2026
- **Medium Article:** N/A — conceptual room, GitHub notes only

---

## Traditional Computer Types

| Type | Screen & Keyboard | Main Purpose |
|------|-------------------|---------------|
| **Laptop** | Yes | Portable everyday computing |
| **Desktop** | Yes | Sustained performance at a fixed location |
| **Workstation** | Yes | Precision and reliability for professional tasks |
| **Server** | No | Providing services to many users over a network |

### Key Distinctions:
- **Desktops** → designed for **consistency**, not mobility
- **Laptops** → built for **portability**; staying cool in a small, battery-powered device is genuinely difficult engineering
- **Workstations** → prioritize **accuracy and reliability**, using specialized components to reduce errors during long/complex computations (e.g. CAD, video rendering, scientific computing)
- **Servers** → run **continuously**, answering requests from multiple users simultaneously — no screen/keyboard needed since they're managed remotely

---

## Other Computer Form Factors

| Type | What It Is | Examples |
|------|-----------|----------|
| **Smartphone** | Pocket-sized computer optimized for battery life and connectivity | iPhone, Android |
| **Tablet** | Touch-first computer with larger screen | iPad, drawing tablet |
| **IoT Device** | Network-connected device with a single purpose | Smart thermostat, doorbell, fitness tracker |
| **Embedded Computer** | Computer built into another device | Coffee maker controller, door sensor, lamp dimmer chip |

---

## IoT vs Embedded Computer — Key Difference

Both can be small and single-purpose. **The difference is connectivity.**

| | IoT Device | Embedded Computer |
|---|-----------|---------------------|
| Network connection | Yes — reports data or receives commands | Often none |
| Awareness | Connected to broader systems | Works in isolation, often for years unnoticed |
| Example | Smart doorbell sending alerts to your phone | Lamp dimmer chip controlling brightness internally |

---

## Core Trade-offs in Computing

### Mobility costs power
Smaller, portable computers must sacrifice sustained performance to save battery and manage heat in a compact form factor.

### Reliability costs money
Servers and critical systems use **redundancy** — extra power supplies, extra disks (RAID), backup components — specifically to avoid failure.

### Purpose shapes everything
- You **touch** a phone (direct interaction)
- You **ask** a server for information (remote request)
- An IoT device works **quietly** without demanding attention (background operation)

---

## Security Relevance

Different computer types = different attack surfaces:

| Type | Common Security Concerns |
|------|---------------------------|
| Servers | DDoS, unauthorized remote access, privilege escalation |
| IoT devices | Weak/default credentials, lack of patching, botnet recruitment (e.g. Mirai botnet) |
| Embedded systems | Firmware vulnerabilities, physical access attacks, rarely updated |
| Smartphones | App-based malware, phishing, OS-level exploits |

**Real-world relevance:** IoT devices are notoriously insecure because manufacturers prioritize cost and functionality over security — this is why IoT botnets (like Mirai) have been used in some of history's largest DDoS attacks.

---

## Key Takeaway
> **"There is no best computer. There is only the right tool for the job."**

Every computer type makes deliberate trade-offs — mobility vs power, cost vs reliability, connectivity vs isolation. Understanding these trade-offs helps identify *why* certain devices are more vulnerable than others, and where security priorities should focus (e.g. IoT devices often need extra scrutiny precisely because they prioritize convenience over security).
