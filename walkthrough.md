# 🧪 DVWA Exploit Walkthrough

This walkthrough documents the steps taken to exploit several common web vulnerabilities using **Damn Vulnerable Web Application (DVWA)** on **Kali Linux**.  
All tests were performed with DVWA security level set to **Low**.

---

## 1️⃣ SQL Injection

**Target:** `http://localhost/dvwa/vulnerabilities/sqli/`  
**Screenshot:** [`screenshots/sql-injection-success.png`](./screenshots/sql-injection-success.png)

### 🔹 Payload:
```sql
1' OR '1'='1
````

### ✅ Result:

The SQL query is manipulated to return all rows from the users table. All usernames and details are displayed on the screen, bypassing authentication or filtering.

---

## 2️⃣ Cross-Site Scripting (XSS) – Stored

**Target:** `http://localhost/dvwa/vulnerabilities/xss_s/`
**Screenshot:** [`screenshots/xss-alert-box.png`](./screenshots/xss-alert-box.png)

### 🔹 Payload:

```html
<script>alert('XSS')</script>
```

### ✅ Result:

The script is stored in the guestbook and executed every time the page loads. This confirms that user input is not properly sanitized, allowing for stored XSS attacks.

---

## 3️⃣ Command Injection

**Target:** `http://localhost/dvwa/vulnerabilities/exec/`
**Screenshot:** [`screenshots/command-injection.png`](./screenshots/command-injection.png)

### 🔹 Payload:

```bash
127.0.0.1; whoami
```

### ✅ Result:

The web app runs system commands by concatenating user input directly into a shell command. This payload appends `whoami`, revealing the web server's execution user (typically `www-data`).

---

## 4️⃣ Brute Force Login

**Target:** `http://localhost/dvwa/vulnerabilities/brute/`
**Screenshot:** [`screenshots/brute-force-found.png`](./screenshots/brute-force-found.png)

### 🔹 Method:

* Username: `admin`
* Tried multiple common passwords manually. Correct Password: **Password**. Also tried "1234, admin, etc..."

### ✅ Result:

After trying multiple guesses, the correct password was discovered, and the app redirected to a protected page.
---

## 🧠 Tools Used

* 🐧 Kali Linux (local VM)
* 🌐 Firefox / Chromium
* 🐍 Custom payloads via browser inputs

---

## ⚠️ Disclaimer

This project was completed in a **local environment for educational purposes only**. All tests were done ethically on a legal, self-hosted system. Do not use these techniques without explicit permission on other networks or systems.
