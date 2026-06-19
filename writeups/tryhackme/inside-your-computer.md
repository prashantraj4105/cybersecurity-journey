# Inside Your Computer — TryHackMe

- **Platform:** TryHackMe
- **Room:** Inside Your Computer
- **Date Completed:** June 19, 2026
- **Medium Article:** N/A — conceptual room, GitHub notes only

---

## Why Understand Hardware Before Securing It?
You can't secure what you don't understand. Before learning system security, understanding the actual physical components and boot process is foundational.

---

## Core Computer Components — With Body Analogies

| Component | Function | Analogy |
|-----------|----------|---------|
| **Motherboard** | Connects all components together | Skeleton + Nervous System |
| **PSU** (Power Supply Unit) | Supplies power to all components | Heart — pumps electricity |
| **CPU** | Executes instructions and calculations | Brain |
| **Network Card** | Enables communication with outside world | Vocal cords — interacts with environment |
| **GPU** | Processes images/graphics | Visual cortex |
| **RAM** | Volatile memory — temporary working data | Short-term memory |
| **SSD/HDD** | Non-volatile storage — permanent data | Long-term memory |
| **I/O Devices** | Mouse, speaker, microphone, keyboard | Senses (touch, hearing, etc.) |

**Key distinction:**
- **RAM = Volatile** → data lost when power goes off
- **SSD/HDD = Non-volatile** → data persists even without power

---

## What Happens When You Press the Power Button

### Step 1 — Press the Power Button
- Signal sent to **PSU** → allows power to flow through the system
- **Analogy:** Like waking up — body starts receiving oxygen and pumping blood

### Step 2 — Firmware Starts (UEFI/BIOS)
- Computer's firmware initializes — the **first software that runs**
- **UEFI** (Unified Extensible Firmware Interface) — modern standard
- **BIOS** — older system, mostly replaced by UEFI today, but term still commonly used
- Manages startup of all components, similar to how the body's autonomic system manages waking up

### Step 3 — Power-On Self Test (POST)
- UEFI runs a self-test routine
- Checks if every required component is:
  - **Present**
  - **Configured correctly**
  - **Functioning properly**
- Errors at this stage trigger beep codes or visual alerts

### Step 4 — Select Boot Device
- UEFI holds an **ordered priority list** of devices to check for the OS boot routine
- Typically checks SSD/HDD first (wherever OS is installed)
- Can be configured to boot from USB, network, etc.

### Step 5 — Initiate Bootloader
- Bootloader **transfers the Operating System** from the boot device into **RAM**
- Once OS is loaded into RAM, **UEFI hands control over to the OS**
- This completes the boot sequence

---

## Complete Boot Sequence Flow

```
Press Power Button
        ↓
Firmware Starts (UEFI/BIOS)
        ↓
POST (Power-On Self Test)
        ↓
Select Boot Device
        ↓
Initiate Bootloader → OS loads into RAM
        ↓
UEFI hands control to OS
```

---

## Why This Matters for Security

Understanding the boot process is critical because several real-world attacks target this exact sequence:

- **Bootkit/Rootkit attacks** — malware that infects the boot process before the OS even loads, making it extremely hard to detect
- **UEFI/BIOS attacks** — firmware-level malware that persists even after OS reinstallation
- **Boot device tampering** — attacker changes boot priority to load malicious OS from USB
- **Cold boot attacks** — extracting data from RAM immediately after power-off, since RAM retains data briefly

Security tools like **Secure Boot** exist specifically to verify that only trusted, signed software runs during this boot sequence — preventing bootkits from loading.


---

## Key Takeaways
1. Every hardware component has a specific role — understanding them is the foundation of system security
2. RAM is volatile (temporary), SSD/HDD is non-volatile (permanent)
3. Boot sequence: Power → Firmware (UEFI) → POST → Select Boot Device → Bootloader → OS takes control
4. UEFI has mostly replaced BIOS but performs the same fundamental role
5. POST catches hardware failures before the OS even attempts to load
6. The boot process is a real attack surface — bootkits and firmware attacks target this exact sequence
