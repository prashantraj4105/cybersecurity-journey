# Client Server Basics — TryHackMe

- **Platform:** TryHackMe
- **Room:** Client Server Basics
- **Date Completed:** June 2026
- **Method:** YouTube walkthrough + notes
- **Medium Article:** N/A — conceptual room, GitHub notes only

---

## What is Client-Server Architecture?
A model that facilitates **sharing resources through interconnection** — different devices communicate across a network using defined roles.

| Role | Function |
|------|----------|
| **Client** | Browser — requests the webpage/resource |
| **Server** | Serves/responds to the client's request |

The **server fulfills the client's request** — this is the foundational model behind almost all web communication.

---

## Key Concepts

### Protocol
Defines the **rules** for how a client requests something and how a server responds.
- Examples: HTTP, HTTPS, FTP, DNS

### Port
Identifies **which specific service** is running on a computer/server.
- A single server can run multiple services simultaneously, each on a different port
- Example: Web server on port 80/443, SSH on port 22, FTP on port 21

**Hinglish note:** Port batata hai ki "yeh wala service computer ke kis specific point pe run ho raha hai" — jaise ek building mein alag-alag rooms (ports) mein alag-alag departments (services) baithe hote hain.

### DNS
Converts **domain name → IP address** (covered in detail in the DNS in Detail room)

---

## Practical — Web Communication with curl

```bash
curl -I -v http://httpdemo.local:8080
```

| Flag | Meaning |
|------|---------|
| `-I` | Fetch headers only (HEAD request) — no body content |
| `-v` | Verbose mode — shows full request/response details including connection process |

**Why curl matters in security:**
`curl` is one of the most used command-line tools for web reconnaissance. It lets you:
- Inspect headers without loading a full page
- Test API endpoints
- Check server responses without a browser
- Script automated requests (as seen in earlier Metasploit automation scripts)

---

## URL Component Breakdown — Practical Example

Given: `https://www.iamlearning.thm/contact`

| Component | Value |
|-----------|-------|
| **Schema** | `https` |
| **Hostname** | `iamlearning.thm` |

This reinforces the URL structure learned in the HTTP in Detail room — every URL breaks down into scheme, host, path, etc.


---

## Key Takeaways
1. Client requests, server responds — the foundational model of nearly all internet communication
2. Protocols define the *rules* of communication; ports define *which service* you're talking to
3. A single machine can run many services simultaneously, each isolated on its own port
4. `curl -I -v` is a quick way to inspect server headers and connection details from the terminal
5. Every URL can be broken into schema + hostname + path — same structure across all web requests
