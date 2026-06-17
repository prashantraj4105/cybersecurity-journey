# How Websites Work — TryHackMe

- **Platform:** TryHackMe
- **Room:** How Websites Work
- **Date Completed:** June 16, 2026
- **Vulnerability Exploited:** HTML Injection
- **Medium Article:** [Read here](https://medium.com/@rajprashantwork/i-turned-a-whats-your-name-field-into-a-malicious-link-my-first-html-injection-aada50600f95?postPublishedType=repub)

---

## How Are Websites Created?

A website request flow:
1. You request a page using a browser (Chrome, Firefox, Safari)
2. A **server** (dedicated computer) processes your request and returns a response

### Two Core Components:
| Component | Role |
|-----------|------|
| **Frontend** | What the browser renders — what you see |
| **Backend** | Server processes the request and returns response |

---

## The 3 Building Blocks of Every Website

| Language | Purpose |
|----------|---------|
| **HTML** | Defines structure |
| **CSS** | Adds styling — makes it look pretty |
| **JavaScript** | Adds interactivity and complex features |

---

## HTML — HyperText Markup Language

The language websites are written in. Built from **elements** (tags).

### Common HTML Elements:
```html
<!DOCTYPE html>  <!-- Declares this is an HTML5 document -->
<html>           <!-- Root element - everything goes inside this -->
<head>           <!-- Page metadata (title, etc.) -->
<body>           <!-- Visible content shown in browser -->
<h1>             <!-- Large heading -->
<p>              <!-- Paragraph -->
<button>         <!-- Clickable button -->
<img>            <!-- Image -->
```

### Attributes:
```html
<p id="example">           <!-- Unique identifier for the element -->
<img src="img/cat.jpg">    <!-- Source of the image -->
<p class="bold-text">      <!-- CSS class for styling -->
```

---

## JavaScript — Making Pages Interactive

Without JavaScript, a page is **static** — no interactivity at all.

### Two ways to add JavaScript:
```html
<!-- Inline within script tags -->
<script>
  document.getElementById("demo").innerHTML = "Hack the Planet";
</script>

<!-- External file -->
<script src="/location/of/javascript_file.js"></script>
```

### Event-driven JavaScript:
```html
<button onclick='document.getElementById("demo").innerHTML = "Button Clicked";'>
  Click Me!
</button>
```

HTML elements can have events like `onclick`, `onhover` that trigger JavaScript execution.

**Practical Task:** Used JavaScript to dynamically change a demo element's content to "Hack the Planet" 

---

## Sensitive Data Exposure

Occurs when a website **doesn't properly protect or remove sensitive clear-text information** visible to end users.

**Where to look:** Page source code — often contains:
- Exposed login credentials
- Hidden links
- API keys accidentally left in comments

**First step in any web security assessment:** Always view page source (`Ctrl+U` / `View Source`) to check what's exposed.

---

## HTML Injection — Practical Exploitation

### What is HTML Injection?
A vulnerability that occurs when **unfiltered user input** is displayed directly on the page.

### Root Cause:
- Website fails to **sanitise user input** (filter malicious text)
- That unsanitised input gets rendered as actual HTML on the page
- Attacker can inject their own HTML/JavaScript code

### How the Vulnerability Worked:
The room had a **"What's your name?"** input field. This input was passed to a JavaScript function and output directly to the page — **without sanitisation**.

This meant: whatever I typed wasn't treated as plain text — it was treated as actual HTML code by the browser.

### My Exploit:
Instead of entering a normal name, I injected:
```html
<a href="http://hacker.com">click here</a>
```

**Result:** Instead of displaying my "name" as text, the page rendered a **fully clickable malicious link** — exactly as if the website's developer had put it there themselves.

### Why This Matters:
In a real attack scenario, this could be used to:
- Create fake login links that redirect to phishing pages
- Inject fake "Click here to verify your account" buttons
- Combine with JavaScript for more advanced attacks (leading toward XSS)
- Deface the website's appearance entirely

### The Golden Rule:
> **Never trust user input.**

Every form field, URL parameter, or input box is a potential injection point unless the application properly sanitises and encodes the data before rendering it.

---


## Key Takeaways
1. Websites = Frontend (HTML/CSS/JS) + Backend (server processing)
2. HTML defines structure, CSS styles it, JavaScript makes it interactive
3. Sensitive data exposure often hides in plain sight — always check page source
4. HTML Injection happens when user input is rendered without sanitisation
5. Unsanitised input can be weaponised — I turned a "name" field into a malicious clickable link
6. The fix: always sanitise and encode user input before displaying it back on a page
7. This is the foundational concept behind much more dangerous attacks like XSS
