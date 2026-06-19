# Putting It All Together — TryHackMe

- **Platform:** TryHackMe
- **Room:** Putting It All Together
- **Date Completed:** June 19, 2026
- **Flag:** THM{YOU_GOT_THE_ORDER}
- **Task:** Arrange the complete request flow in correct order
- **Medium Article:** [Read here](https://medium.com/@rajprashantwork)

---

## The Big Picture
This room connects everything learned so far — DNS, HTTP, Networking — into **one complete journey**: what actually happens between typing a URL and seeing a webpage.

---

## The Complete Request Flow (Correct Order)

### Phase 1 — DNS Resolution
```
1. Request tryhackme.com in your browser
2. Check Local Cache for IP Address
3. Check your recursive DNS Server for Address
4. Query root server to find authoritative DNS Server
5. Authoritative DNS server advises the IP address for the website
```

### Phase 2 — Security & Traffic Management
```
6. Request passes through a Web Application Firewall (WAF)
7. Request passes through a Load Balancer
```

### Phase 3 — Server Processing
```
8. Connect to Webserver on port 80 or 443
9. Web server receives the GET request
10. Web Application talks to Database
```

### Phase 4 — Response
```
11. Your Browser renders the HTML into a viewable website
```

**Flag captured for arranging correctly:** `THM{YOU_GOT_THE_ORDER}` ✅

---

## Component Deep Dive

### Load Balancer
Solves 2 problems:
- **High traffic handling** — distributes load across multiple servers
- **Failover** — if one server goes down, traffic reroutes automatically

**How it decides which server handles a request:**
| Algorithm | Logic |
|-----------|-------|
| Round-robin | Distributes requests evenly, one by one, in sequence |
| Weighted | Sends more requests to servers with lower current workload |

Load balancer also performs **health checks** — continuously verifies each server is running properly before sending it traffic.

---

### CDN — Content Delivery Network
- Hosts **static files** (JS, CSS, Images, Videos) across thousands of servers worldwide
- When a user requests a file, CDN finds the **physically nearest server** and serves from there
- Reduces load on the origin server and improves speed for users far from the main server

**Example:** A user in India requesting an image hosted on a US server — CDN serves it from a nearby Indian server instead, instead of routing all the way to the US.

---

### Databases
- Web servers communicate with databases to **store and retrieve data**
- Range from simple flat text files to complex **multi-server clusters** for speed and resilience

---

### WAF — Web Application Firewall
- Sits **between the request and the web server**
- Primary purpose: protect the server from **hacking attempts and DoS attacks**
- Performs **rate limiting** — only allows a certain number of requests per IP per second
- If a request looks like a potential attack → **dropped immediately**, never reaches the web server

---

## How Web Servers Actually Work

A web server = software that listens for incoming connections and delivers content using HTTP.

### Common Web Server Software:
| Software | Root Directory |
|----------|----------------|
| Apache / Nginx | `/var/www/html` |
| IIS (Windows) | `C:\inetpub\wwwroot` |
| NodeJS | Custom (app-defined) |

**Example:** Requesting `http://www.example.com/picture.jpg` → server fetches `/var/www/html/picture.jpg` and returns it.

---

### Virtual Hosts
- Allows **one server to host multiple websites** with different domain names
- Server checks the **`Host` header** in the HTTP request to determine which website's content to serve

---

## Static vs Dynamic Content

| Type | Behavior |
|------|----------|
| **Static** | Never changes — same content every request (e.g. logo image, CSS file) |
| **Dynamic** | Changes based on request — generated fresh each time (e.g. personalized pages) |

---

## Frontend vs Backend — The PHP Example

```php
<html><body>Hello <?php echo $_GET["name"]; ?></body></html>
```

What the **client actually sees** (after backend processing):
```html
<html><body>Hello adam</body></html>
```

**Key insight:** The client **never sees the PHP code**. All backend processing happens invisibly on the server — only the final HTML result is sent to the browser.

### Why This Matters for Security:
This server-side processing — taking user input (`$_GET["name"]`) and inserting it into output — is **exactly** the same pattern that causes:
- HTML Injection (if `name` isn't sanitised)
- SQL Injection (if `name` goes into a database query)
- Command Injection (if `name` is passed to system commands)

The backend is invisible to the client, which is precisely why **backend vulnerabilities are harder to detect from the outside** — you can't view-source your way to finding them. This is where tools like Burp Suite and manual testing techniques become essential.

---
## Key Takeaways
1. A single webpage request involves DNS, WAF, Load Balancer, Web Server, and Database — multiple layers working together
2. Load balancers use round-robin or weighted algorithms to distribute traffic
3. CDNs serve static content from the geographically nearest server
4. WAF filters malicious requests before they ever reach the actual server
5. Backend code (PHP, etc.) is invisible to the client — only output HTML is sent
6. This invisible backend processing is exactly where injection vulnerabilities originate
7. Understanding the full request pipeline helps identify where security controls should be applied
