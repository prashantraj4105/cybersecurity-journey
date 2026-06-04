# Defensive Security Intro — TryHackMe

- **Platform:** TryHackMe  
- **Room:** Defensive Security Intro  
- **Date Completed:** June 4, 2026  
- **Flag:** THM{THREAT-BLOCKED}  
- **Medium Article:** [Read here](https://medium.com/@rajprashantwork/i-investigated-my-first-cyber-attack-heres-what-a-soc-analyst-actually-does-81f12e9a1c00)

---

## What is Defensive Security?

While offensive security focuses on finding and exploiting vulnerabilities (Red Team), defensive security is about preventing attacks and detecting/responding when they occur. This is the Blue Team.

Blue Team work includes:
- Cybersecurity awareness
- Asset documentation and management
- System patching and updates
- Setting up firewalls and IPS
- Log monitoring and alerting

---

## Key Areas Covered

### SOC — Security Operations Center
Team that monitors network 24/7 for malicious events:
- Vulnerability detection
- Policy violation monitoring
- Unauthorized activity detection
- Network intrusion detection

### DFIR — Digital Forensics and Incident Response
Investigates attacks after they occur:
- File system analysis
- Memory imaging
- Network and system log analysis

**Incident Response Steps:**
1. Preparation
2. Detection and Analysis
3. Containment, Eradication, and Recovery
4. Post-Incident Activity

### Malware Analysis
- **Static Analysis** — examining malware without running it
- **Dynamic Analysis** — running in controlled environment and monitoring behavior

**Malware Types:**
- Virus — slows system, deletes/overwrites files
- Trojan Horse — disguises as legitimate software
- Ransomware — encrypts files, demands payment

---

## Practical Exercise — SOC Analyst at a Bank

**Tool used:** SIEM (Security Information and Event Management)

### Step 1 — Threat Detection in SIEM
Alert log showed suspicious activity from IP `143.110.250.149`:
- 10:44 — Unauthorized SSH connection attempt to port 22
- 10:47 — **Successful SSH authentication** from same IP

Pattern = brute force followed by successful breach (3 min gap = red flag)

### Step 2 — IP Reputation Check
Used IP scanner (real world = AbuseIPDB / Cisco Talos):
- Result: **100% malicious confidence**
- ISP: China Mobile Communications Corporation
- Country: China, Zhenjiang, Jiangsu

### Step 3 — Incident Escalation
Escalated to **SOC Team Lead** (Will Griffin)
- Not Sales Executive — wrong department
- Not Security Consultant — not in direct chain of command
- SOC Team Lead = correct authority for active incidents

### Step 4 — Firewall Block
Added `143.110.250.149` to firewall block list

**Flag received:** `THM{THREAT-BLOCKED}` ✅

---

## Key Takeaways

1. Defensive security requires active monitoring and quick response
2. SIEM is the backbone of SOC analyst work
3. Threat intelligence tools (AbuseIPDB, Cisco Talos) are used daily
4. Escalation chain knowledge is as important as technical skills
5. Incident response follows a structured cycle
