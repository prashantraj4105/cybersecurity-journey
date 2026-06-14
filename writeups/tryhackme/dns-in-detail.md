# DNS in Detail — TryHackMe

- **Platform:** TryHackMe
- **Room:** DNS in Detail
- **Date Completed:** June 14, 2026
- **Flag:** THM{7012BBA60997F35A9516C2E16D2944FF}
- **Medium Article:** [Read here](https://medium.com/@rajprashantwork/i-found-a-hidden-flag-inside-a-dns-record-heres-how-dns-actually-works-c3f7ad781aaf?postPublishedType=initial)

---

## What is DNS?
DNS = **Domain Name System**

Every device on a network is identified by an IP address — but remembering a 32-bit number like `104.26.10.229` for every website is impossible.

DNS converts human-readable **domain names** (like google.com) into their corresponding **IP addresses**.

---

## Domain Name Structure

```
jupiter.servers.tryhackme.com
│         │         │        │
│         │         │        └── TLD (.com)
│         │         └─────────── Second-Level Domain (tryhackme)
│         └───────────────────── Subdomain (servers)
└─────────────────────────────── Subdomain (jupiter)
```

### TLD — Top Level Domain
The **rightmost part** of a domain name.

Two types:
- **gTLD** (Generic TLD) — based on purpose:
  - `.com` → commercial
  - `.org` → organisation
  - `.edu` → education
  - `.gov` → government
- **ccTLD** (Country Code TLD) — based on geography:
  - `.ca` → Canada
  - `.co.uk` → United Kingdom
  - `.in` → India

Over **2000 TLDs** exist today.

### Second-Level Domain
- `tryhackme` in `tryhackme.com`
- Max **63 characters** + TLD
- Only `a-z`, `0-9`, and hyphens allowed

### Subdomain
- Sits on the **left** of second-level domain
- `jupiter` in `jupiter.servers.tryhackme.com`
- Max length of subdomain = **63 characters**
- Total domain length must be **253 characters or less**

---

## DNS Record Types

### A Record
- Resolves domain to **IPv4 address**
- Example: `website.thm → 10.10.10.10`

```bash
nslookup --type=A www.website.thm
# Output: Address: 10.10.10.10
```

### AAAA Record
- Resolves domain to **IPv6 address**
- Example: `2606:4700:20::681a:be5`

### CNAME Record (Canonical Name)
- Resolves domain to **another domain name** (not an IP)
- Example: `shop.website.thm → shops.myshopify.com`
- Then another DNS request is made to resolve `shops.myshopify.com` to its IP

```bash
nslookup --type=CNAME shop.website.thm
# Output: shop.website.thm canonical name = shops.myshopify.com
```

**Analogy:** CNAME is like a redirect sign — "Go to this other address instead."

### MX Record (Mail Exchanger)
- Directs **email traffic** to the correct mail server
- Example: `tryhackme.com → alt1.aspmx.l.google.com`
- Comes with a **priority flag** — lower number = higher priority
- If primary mail server goes down → email goes to backup server automatically

```bash
nslookup --type=MX website.thm
# Output: website.thm mail exchanger = 30 alt4.aspmx.l.google.com
```

**Analogy:** MX record is like a post office directory — "Send all letters for this company to THIS post office. If that's closed, use the backup."

Priority 10 = primary, Priority 30 = backup. Lower number = higher priority.

### TXT Record
- **Free text field** — any text-based data can be stored
- Common uses:
  - Domain ownership verification (Google, Microsoft)
  - Email spam prevention (SPF, DKIM records)
  - Storing flags in CTF challenges 

```bash
nslookup --type=TXT website.thm
# Output: website.thm text = "THM{7012BBA60997F35A9516C2E16D2944FF}"
```

**Real world examples:**
- Google verifies you own a domain by asking you to add a specific TXT record
- SPF records in TXT tell mail servers which IPs are allowed to send email for a domain

---

## What Happens When You Make a DNS Request

Step by step journey of `google.com`:

```
1. Check LOCAL CACHE
   → Already visited recently? Use cached IP. Done.
   ↓ (if not found)

2. RECURSIVE DNS SERVER (provided by your ISP)
   → Checks its own cache
   ↓ (if not found)

3. ROOT SERVER
   → Backbone of internet DNS
   → Doesn't know the IP but knows which TLD server to ask
   → "Go ask the .com TLD server"
   ↓

4. TLD SERVER (.com server)
   → Knows which Authoritative Name Server handles google.com
   → "Go ask Google's name server"
   ↓

5. AUTHORITATIVE NAME SERVER
   → Stores all actual DNS records for google.com
   → Returns the IP address
   ↓

6. Recursive DNS server caches the result (for TTL duration)
   → Sends IP back to your device
```

### TTL — Time To Live
- Specifies **how long** a DNS record should be **cached** (in seconds)
- Example: TTL = 3600 → cached for 1 hour
- After TTL expires → fresh DNS lookup required

---

## Practical — nslookup Commands Used

```bash
# A Record — get IPv4 address
nslookup --type=A www.website.thm

# AAAA Record — get IPv6 address
nslookup --type=AAAA website.thm

# CNAME — get canonical name
nslookup --type=CNAME shop.website.thm

# MX Record — get mail server
nslookup --type=MX website.thm

# TXT Record — get text records (flag found here!)
nslookup --type=TXT website.thm
```

**Flag captured:** `THM{7012BBA60997F35A9516C2E16D2944FF}` ✅

---

## Key Takeaways
1. DNS converts domain names to IP addresses — humans remember names, machines use IPs
2. Domain structure: Subdomain → Second-Level Domain → TLD
3. A = IPv4, AAAA = IPv6, CNAME = another domain, MX = mail, TXT = free text
4. DNS lookup: Cache → Recursive → Root → TLD → Authoritative
5. TTL controls how long a DNS record stays cached
6. TXT records used for verification, spam prevention, and yes — CTF flags!
