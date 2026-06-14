# Extending Your Network — TryHackMe

- **Topic:** Port Forwarding, Firewalls, VPN, Switches, VLAN
- **Date Completed:** June 13, 2026
- **Method:** YouTube walkthrough (paid room) + notes
- **Medium Article:** N/A — conceptual room, GitHub notes only

---

## Port Forwarding
- If a service runs on **port 80** inside a network, it is only accessible to devices **within** that network
- To make it accessible over the internet (e.g. a web server), **port forwarding** is required
- Port forwarding **opens specific ports** on the router
- Configured at the **router level**

**Simple analogy:**
Building ke andar ek room hai — sirf andar waale ja sakte hain. Port forwarding ek specific darwaza kholta hai jisse baahri log bhi aa sakein.

---

## Firewalls
A device that **determines what traffic is allowed or denied** in/out of a network.

### How Firewalls Work:
Firewalls do **packet inspection** to check:
- Where is traffic **coming from**?
- Where is it **going**?
- Which **port** is it using?
- Which **protocol** is it using?

Firewalls can be **hardware** or **software** based.

---

### 2 Primary Categories:

#### Stateful Firewall
- Determines behaviour based on the **entire connection** — not just individual packets
- Decision making is **dynamic**
- Uses **more resources** than stateless
- If a connection from a host is determined bad → **entire device is blocked**
- Smarter but resource-heavy

#### Stateless Firewall
- Follows **static/fixed rules** to identify if a specific packet is allowed or not
- A bad packet doesn't necessarily mean the device is bad
- **Great at handling large volumes** of traffic (e.g. DDoS attacks)
- **Dumber** — rules are fixed, less intelligent
- Uses fewer resources

| Feature | Stateful | Stateless |
|---------|----------|-----------|
| Decision based on | Entire connection | Individual packets |
| Resources | High | Low |
| Intelligence | Dynamic | Fixed rules |
| Best for | General traffic | DDoS protection |

**Firewalls operate at OSI Layer 3 (Network) and Layer 4 (Transport)**

**Example:**
If IP `198.51.100.34` is continuously sending bad packets → add a rule to drop all packets from that IP → system stays protected.

---

## VPN — Virtual Private Network
Creates a **private network over a public network (internet)** for secure communication.

### What VPN does:
- Allows devices in **different geographical locations** to connect securely
- Provides **privacy and anonymity**
- Encrypts traffic between endpoints

**TryHackMe uses VPN** to give access to vulnerable machines — so those machines are not exposed directly to the internet.

---

### VPN Technologies:

#### PPP + PPTP (Point-to-Point Tunneling Protocol)
- Uses PPP for **authentication**
- Provides **encryption**
- **Easy to set up**
- **Weakly encrypted** compared to modern alternatives

#### IPSec (Internet Protocol Security)
- Encrypts data using **existing internet protocol framework**
- Much **stronger encryption** than PPTP
- Harder to set up but more secure
- Widely used in enterprise VPNs

| VPN Type | Encryption | Setup | Use |
|----------|-----------|-------|-----|
| PPTP | Weak | Easy | Legacy/basic |
| IPSec | Strong | Complex | Enterprise |

---

## LAN Networking Devices

### Router
- Connects **different networks** and passes data between them
- Operates at **OSI Layer 3 (Network Layer)**
- Finds the **optimal path** for data to travel using routing protocols

---

### Switch
- Dedicated networking device for connecting **multiple devices** within a network
- Can connect **3 to 63 devices** via Ethernet cables
- Operates at **Layer 2 and/or Layer 3** of OSI model
- Layer 2 and Layer 3 switches are **exclusive** — a Layer 2 switch cannot operate at Layer 3

#### Layer 2 Switch
- Forwards **frames** to devices using **MAC addresses**
- IP protocol is stripped — works only with MAC
- Standard switch used in most LANs

#### Layer 3 Switch
- More sophisticated — can do **some responsibilities of a router**
- Can both:
  - Send **frames** to devices (like Layer 2)
  - **Route packets** to other networks using IP protocol
- Useful in large enterprise networks

| Feature | Layer 2 Switch | Layer 3 Switch |
|---------|---------------|----------------|
| Operates on | MAC address | MAC + IP |
| Routing | No | Yes (limited) |
| Use case | Simple LAN | Large networks |

---

### VLAN — Virtual Local Area Network
- Allows specific devices within a network to be **virtually split** into separate groups
- All devices can still share internet connection but are **treated separately**
- Provides **security through network segregation** — rules determine how specific devices communicate

**Example use case:**
Office network — HR, Finance, and Engineering departments on same physical network but on different VLANs so they can't access each other's data.

---

## Key Takeaways
1. Port forwarding opens specific router ports to allow external access to internal services
2. Stateful firewalls are smarter but heavier; stateless are faster but dumber
3. Firewalls work at Layer 3 and Layer 4
4. VPN creates encrypted tunnel over public internet — IPSec > PPTP for security
5. Layer 2 switch uses MAC; Layer 3 switch can also route using IP
6. VLAN virtually separates devices on same physical network for security
7. TryHackMe itself uses VPN to protect vulnerable lab machines
