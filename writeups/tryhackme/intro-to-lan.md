# Intro to LAN — TryHackMe

- **Platform:** TryHackMe
- **Room:** Intro to LAN
- **Date Completed:** June 9, 2026
- **Method:** YouTube walkthrough (paid room) + notes
- **Medium Article:** N/A — conceptual room, no hands-on flags

---

## LAN — Local Area Network
A network that connects devices within a limited area (home, office, campus).
Design of how a network looks and functions = **Topology**

---

## Network Topologies

### 1. Ring Topology (Token Topology)
- All devices connect to two adjacent devices forming a complete circle
- Data travels in **one direction only**
- If any single connection breaks → entire network fails
- Easy to troubleshoot but single point of failure
- Not commonly used today

### 2. Bus Topology
- All devices connect to a **single backbone cable**
- Data sent in both directions along the backbone until destination reached
- Cannot handle large amounts of data packets
- **Cost efficient** — cheap to set up
- Backbone failure = entire network down
- Was common in early networks, rare today

### 3. Star Topology (Most Common Today)
- All devices connect to a **centralized switch or hub**
- If central device fails → entire network goes down
- Most reliable and scalable design
- More expensive than bus or ring
- **Scalability is directly proportional to maintainability**
- Used in almost all modern LANs

---

## Key Networking Devices

### Switch
- Aggregates multiple devices using ethernet cables
- Available in port sizes: 4, 8, 16, 24, 32 ports
- Tracks which devices are connected on which port (MAC address table)
- Connected to routers — if one path goes down, finds another path
- Operates at **Data Link Layer (Layer 2)**

### Router
- Connects **two or more different networks** together
- **Routing** = process of finding the best path to send data across networks
- Operates at **Network Layer (Layer 3)**
- In star topology: Switch → Router → Internet

---

## Subnetting
Splitting a large network into smaller, more manageable sub-networks.

An IP address serves three purposes in subnetting:

| Purpose | Example | Description |
|---------|---------|-------------|
| Network Address | 192.168.1.0 | Identifies the network |
| Host Address | 192.168.1.100 | Identifies the specific device |
| Default Gateway | 192.168.1.1 | Address used to send data to another network |

**Example:**
- IP: `192.168.1.100` belongs to network `192.168.1.0`
- Default gateway: `192.168.1.1` (usually the router)

---

## ARP Protocol — Address Resolution Protocol
ARP links **MAC addresses** (physical) to **IP addresses** (logical).

### How ARP Works:
1. **ARP Request** — Device broadcasts to entire network:
   - SRC MAC: `01:00:AB:78:99:33`
   - DST MAC: `FF:FF:FF:FF:FF:FF` (broadcast — everyone receives)
   - Message: *"Who has IP address 192.168.1.10?"*

2. **ARP Reply** — Device with matching IP responds directly:
   - SRC MAC: `18:AC:33:12:88:29`
   - DST MAC: `01:00:AB:78:99:33` (back to requester only)
   - Message: *"I have IP address 192.168.1.10"*

3. Result stored in **ARP cache** for future use

> MAC address = physical identifier
> IP address = logical identifier
> ARP = the bridge between the two

---

## DHCP — Dynamic Host Configuration Protocol
Automatically assigns IP addresses to devices on a network.

IP can be assigned two ways:
- **Manually** — admin sets it (static IP)
- **Automatically** — via DHCP server (dynamic IP)

### DHCP 4-Step Process (DORA):

| Step | Direction | Message |
|------|-----------|---------|
| **Discover** | Device → Network | "Hey, I'm new here. Anyone give me an IP?" |
| **Offer** | DHCP Server → Device | "Sure! You can have 192.168.1.10" |
| **Request** | Device → DHCP Server | "Yes, I'll take 192.168.1.10" |
| **ACK** | DHCP Server → Device | "Confirmed. Use it for the next 24 hours." |

---


## Key Takeaways
1. Star topology is dominant today — reliable but central point of failure
2. Switches work at Layer 2 (MAC), Routers work at Layer 3 (IP)
3. ARP resolves IP → MAC using broadcast + unicast reply
4. DHCP automates IP assignment via 4-step DORA process
5. Subnetting divides networks for efficiency and security
6. Default gateway is the exit point from your local network
