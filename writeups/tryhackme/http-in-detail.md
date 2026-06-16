# HTTP in Detail — TryHackMe

- **Platform:** TryHackMe
- **Room:** HTTP in Detail
- **Date Completed:** June 15, 2026
- **Flags Captured:** 6 flags
  - `THM{YOU'RE_IN_THE_ROOM}` — GET /room
  - `THM{YOU_FOUND_THE_BLOG}` — GET /blog?id=1
  - `THM{USER_IS_DELETED}` — DELETE /user/1
  - `THM{USER_HAS_UPDATED}` — PUT /user/2
  - `THM{HTTP_REQUEST_MASTER}` — POST /login
  - `THM{INVALID_HTTP_CERT}` — HTTP vs HTTPS
- **Medium Article:** [Read here](https://medium.com/@rajprashantwork)

---

## What is HTTP?
**HTTP = HyperText Transfer Protocol**
- Developed by **Tim Berners-Lee** and his team
- Set of rules for communicating with web servers
- Transfers webpage data — HTML, images, videos, etc.

## What is HTTPS?
**HTTPS = HyperText Transfer Protocol Secure**
- Secure version of HTTP
- Data is **encrypted** — nobody can intercept what you send/receive
- Verifies you're talking to the **correct web server** (not an impersonator)
- Uses SSL/TLS certificates — if invalid → flag `THM{INVALID_HTTP_CERT}`

---

## URL Structure — Uniform Resource Locator

```
http://user:password@tryhackme.com:80/view-room?id=1#task3
  │        │               │         │      │        │    │
Scheme    User           Host      Port   Path   Query  Fragment
```

| Part | Example | Description |
|------|---------|-------------|
| **Scheme** | `http://` | Protocol to use (HTTP, HTTPS, FTP) |
| **User** | `user:password@` | Optional authentication credentials |
| **Host** | `tryhackme.com` | Domain name or IP of the server |
| **Port** | `:80` | Port to connect (80=HTTP, 443=HTTPS) |
| **Path** | `/view-room` | File or resource location |
| **Query String** | `?id=1` | Extra parameters sent to the path |
| **Fragment** | `#task3` | Reference to a specific location on the page |

---

## Making an HTTP Request

Simplest possible request — just one line:
```
GET / HTTP/1.1
```

Full example request with headers:
```
GET / HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/
```

- Every request ends with a **blank line** to tell server the request is finished
- Extra info sent in **headers**

Example response:
```
HTTP/1.1 200 OK
Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98

<html>
<head><title>TryHackMe</title></head>
<body>Welcome To TryHackMe.com</body>
</html>
```

---

## HTTP Methods

| Method | Use | Example |
|--------|-----|---------|
| **GET** | Retrieve information | `GET /room HTTP/1.1` |
| **POST** | Submit data / create record | `POST /login` with username+password |
| **PUT** | Update existing information | `PUT /user/2` with new username |
| **DELETE** | Delete a record | `DELETE /user/1` |

---

## Practical Tasks — All Flags Captured

### Task 1 — GET /room
```
GET /room HTTP/1.1
Host: tryhackme.com
```
Response: `Welcome to the Room page THM{YOU'RE_IN_THE_ROOM}` 

### Task 2 — GET /blog?id=1 (Query String)
```
GET /blog?id=1 HTTP/1.1
Host: tryhackme.com
```
Response: `Viewing Blog article 1 THM{YOU_FOUND_THE_BLOG}` 

### Task 3 — DELETE /user/1
```
DELETE /user/1 HTTP/1.1
Host: tryhackme.com
```
Response: `The user has been deleted THM{USER_IS_DELETED}` 

### Task 4 — PUT /user/2
```
PUT /user/2 HTTP/1.1
Host: tryhackme.com
username=admin
```
Response: `Username changed to admin THM{USER_HAS_UPDATED}` 

### Task 5 — POST /login
```
POST /login HTTP/1.1
Host: tryhackme.com
Content-Type: application/x-www-form-urlencoded
username=thm&password=letmein
```
Response: `You logged in! Welcome Back THM{HTTP_REQUEST_MASTER}` 

### Bonus — HTTP vs HTTPS
Accessing site over HTTP (no SSL) → `THM{INVALID_HTTP_CERT}` 

---

## HTTP Status Codes

| Range | Category |
|-------|----------|
| 100–199 | Informational |
| 200–299 | Success |
| 300–399 | Redirection |
| 400–499 | Client Errors |
| 500–599 | Server Errors |

### Common Codes:
| Code | Meaning |
|------|---------|
| 200 | OK |
| 201 | Created |
| 301 | Moved Permanently |
| 302 | Found (temporary redirect) |
| 400 | Bad Request |
| 401 | Not Authorised |
| 403 | Forbidden |
| 404 | Page Not Found |
| 405 | Method Not Allowed |
| 500 | Internal Server Error |
| 503 | Service Unavailable |

---

## HTTP Headers

### Request Headers (Client → Server)
| Header | Purpose |
|--------|---------|
| `Host` | Which website you want |
| `User-Agent` | Browser and OS info |
| `Content-Length` | How much data is being sent |
| `Accept-Encoding` | Compression types supported |
| `Cookie` | Saved session data sent back to server |

### Response Headers (Server → Client)
| Header | Purpose |
|--------|---------|
| `Set-Cookie` | Tells browser to save this cookie |
| `Cache-Control` | How long to cache the response |
| `Content-Type` | What type of data is being returned |
| `Content-Encoding` | Compression method used |

---

## Cookies — How Websites Remember You

**Full cookie flow:**
1. Client sends `GET /` request
2. Server responds with HTML + `Set-Cookie: name=adam`
3. Browser saves cookie
4. Every future request — browser sends `Cookie: name=adam` automatically
5. Server recognises you — no need to log in again

**Most common use:** Website **authentication** — keeping you logged in

**Security relevance:** Cookies are a major target in web attacks:
- **Session hijacking** — stealing someone's cookie = stealing their login
- **XSS attacks** — injecting JavaScript to steal cookies
- View cookies in browser → F12 → Developer Tools → Network tab → Cookies

---

## Cybersecurity Relevance

Every web attack involves HTTP:
- **SQL Injection** — manipulating GET/POST parameters
- **XSS** — injecting scripts via HTTP requests
- **IDOR** — changing IDs in GET requests (`/user/1` → `/user/2`)
- **Authentication bypass** — manipulating POST login requests
- **Session hijacking** — stealing Cookie headers

Understanding HTTP requests/responses is the **foundation of all web penetration testing**.

---

## Key Takeaways
1. HTTP = rules for web communication; HTTPS = encrypted version
2. URL has 7 parts: Scheme, User, Host, Port, Path, Query String, Fragment
3. 4 main HTTP methods: GET (read), POST (create), PUT (update), DELETE (delete)
4. Status codes: 2xx=success, 3xx=redirect, 4xx=client error, 5xx=server error
5. Headers carry extra metadata in every request and response
6. Cookies enable persistent authentication — and are a prime attack target
7. Every web attack (SQLi, XSS, IDOR) works through HTTP requests
