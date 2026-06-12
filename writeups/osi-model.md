# OSI Model — TryHackMe / Networking Fundamentals

- **Topic:** OSI Model (Open Systems Interconnection)
- **Date Completed:** June 10, 2026
- **Method:** YouTube walkthrough (paid room) + notes
- **Medium Article:** N/A — conceptual room, GitHub notes only

---

## What is the OSI Model?
A 7-layer conceptual model that defines **how devices over a network share, send, receive, and interpret data**.

Each layer adds its own piece of information to the data as it travels down the stack — this process is called **Encapsulation**.

---

## The 7 Layers (Top to Bottom)

| Layer # | Name | Key Function |
|---------|------|---------------|
| 7 | Application | User-facing protocols (HTTP, DNS, FTP) |
| 6 | Presentation | Translation, encryption, formatting |
| 5 | Session | Connection establishment, synchronization |
| 4 | Transport | Reliable/unreliable delivery (TCP/UDP) |
| 3 | Network | Routing, IP addressing |
| 2 | Data Link | MAC addressing, framing |
| 1 | Physical | Raw bits over cables/media |

**Mnemonic:** *"All People Seem To Need Data Processing"* (Layer 7 → 1)

---

## Layer 7 — Application Layer
- Protocols that decide how end users **see and interact** with sent/received data
- Provides GUI (Graphical User Interface) for interaction
- **Key Protocol — DNS (Domain Name System):**
  Converts a website's **domain name** into its **IP address**
  (e.g. google.com → 142.250.x.x)

---

## Layer 6 — Presentation Layer
- Acts as a **translator** to and from the Application layer
- Handles **data formatting, encoding, and encryption**
- Security features like **HTTPS encryption** are associated with this layer
  (in practice, TLS/SSL encryption operates closer to Transport layer — but conceptually presentation layer handles data translation/formatting)

---

## Layer 5 — Session Layer
- After data is translated by Presentation layer, Session layer **builds a connection** with the other computer
- Once connection is established → **session becomes active**
- **Synchronizes** both computers to ensure data integrity before and after delivery
- Divides data into **chunks (packets)** and sends them one by one
  - Why? If connection is lost, only the missing chunks need to be resent — not the entire data
- **Each session is unique** — data from one session cannot travel into another session

---

## Layer 4 — Transport Layer
Data transmission uses either **TCP** or **UDP** depending on requirements.

### TCP — Transmission Control Protocol
- **Reliable and guaranteed** delivery
- Maintains a **constant connection** between sender and receiver
- Guarantees data is **reassembled correctly** in the order sent by Session layer
- **Slower than UDP** due to connection establishment overhead
- Used for: file sharing, internet browsing, email

### UDP — User Datagram Protocol
- **Not reliable**, no guarantee of delivery — like a postal system (send and forget)
- **Faster than TCP** — no synchronization or connection setup
- Does not maintain a continuous connection like TCP
- Leaves error-checking and control to the **application software**
- Used for: ARP, DHCP, video streaming, gaming

### TCP vs UDP — Quick Comparison
| Feature | TCP | UDP |
|---------|-----|-----|
| Reliability | Guaranteed | Not guaranteed |
| Speed | Slower | Faster |
| Connection | Persistent | Connectionless |
| Use case | File transfer, browsing, email | DHCP, ARP, streaming |

---

## Layer 3 — Network Layer
- Handles **routing** — finding the **best/optimal path** for packets to travel
- Deals with **IP addressing**
- Key Routing Protocols:
  - **OSPF** — Open Shortest Path First
  - **RIP** — Routing Information Protocol

---

## Layer 2 — Data Link Layer
- Focuses on **MAC addresses**
- Every NIC (Network Interface Card) has a unique MAC address
- Data is tagged with MAC address as the **endpoint** — determines exact device data needs to reach
- MAC address **cannot be changed permanently** but **can be spoofed**

---

## Layer 1 — Physical Layer
- The actual physical medium — **Ethernet cables**, fiber, wireless signals
- Transmits data as **raw bits** (0s and 1s)

---

## Encapsulation — How Data Travels

```
Application Data
    ↓ (Layer 7 adds header)
Presentation Data
    ↓ (Layer 6 formats/encrypts)
Session Data
    ↓ (Layer 5 establishes session)
Segments (TCP/UDP header added)
    ↓ (Layer 4)
Packets (IP header added)
    ↓ (Layer 3)
Frames (MAC header added)
    ↓ (Layer 2)
Bits (sent over physical medium)
    ↓ (Layer 1)
```

At the receiving end, this process reverses — called **De-encapsulation**.

---


## Key Takeaways
1. OSI has 7 layers — each adds its own header (encapsulation)
2. DNS works at Application layer — converts domain names to IPs
3. TCP = reliable but slow; UDP = fast but unreliable
4. Network layer = IP + routing; Data Link layer = MAC + framing
5. Session layer breaks data into packets for efficient retransmission
6. Physical layer = raw bits over actual hardware/cables
