# Web Application Security Testing Lab

A hands-on project documenting web application security testing methodology, vulnerabilities discovered, and remediation recommendations. All testing was performed on intentionally vulnerable practice applications in a controlled lab environment.

---

## Objective

To identify and document common web application vulnerabilities including Cross-Site Scripting (XSS), SQL Injection, and Cross-Site Request Forgery (CSRF) using manual testing techniques and Burp Suite.

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Burp Suite | Intercepting and analyzing HTTP requests and responses |
| DVWA (Damn Vulnerable Web App) | Vulnerable target application |
| Firefox / Chrome | Browser-based manual testing |
| OWASP Testing Guide | Methodology reference |

---

## Target Application

**DVWA (Damn Vulnerable Web Application)** — an intentionally vulnerable PHP/MySQL web application designed for security professionals to practice their skills in a legal environment.

> All testing was conducted in a local lab environment on applications designed to be vulnerable. No real systems were tested.

---

## Vulnerabilities Found

| # | Vulnerability | OWASP Category | Severity | CWE |
|---|--------------|----------------|----------|-----|
| 1 | Reflected XSS | A03:2021 — Injection | High | CWE-79 |
| 2 | Stored XSS | A03:2021 — Injection | High | CWE-79 |
| 3 | SQL Injection | A03:2021 — Injection | Critical | CWE-89 |
| 4 | CSRF | A01:2021 — Broken Access Control | Medium | CWE-352 |

---

## Testing Methodology

1. **Reconnaissance** — Mapped all input fields, forms, and parameters in the application
2. **Interception** — Used Burp Suite to intercept and modify HTTP requests
3. **XSS Testing** — Injected JavaScript payloads into input fields and URL parameters
4. **SQL Injection Testing** — Injected SQL syntax into login and search fields
5. **CSRF Testing** — Analyzed forms for missing anti-CSRF tokens
6. **Documentation** — Recorded each finding with payload, screenshot, impact, and fix

---

## Sample Finding 1 — Reflected XSS

**Endpoint:** `GET /vulnerabilities/xss_r/?name=`
**Tool Used:** Burp Suite + Manual

**Payload Injected:**
```html
<script>alert('XSS')</script>
```

**Result:** JavaScript executed in the browser — alert box appeared confirming the vulnerability.

**Impact:** An attacker can craft a malicious URL and trick a victim into clicking it, stealing session cookies or redirecting to a phishing page.

**Remediation:**
- Encode all user-supplied output using HTML entity encoding
- Implement Content Security Policy (CSP) headers
- Validate and sanitize all input server-side

---

## Sample Finding 2 — SQL Injection

**Endpoint:** `POST /vulnerabilities/sqli/`
**Tool Used:** Burp Suite + Manual

**Payload Injected:**
```sql
' OR '1'='1
```

**Result:** Application returned all user records from the database, bypassing authentication logic.

**Impact:** An attacker can extract the entire database, bypass login, modify or delete records.

**Remediation:**
- Use parameterized queries / prepared statements
- Never concatenate user input directly into SQL queries
- Apply principle of least privilege to database accounts

---

## Sample Finding 3 — CSRF

**Endpoint:** `POST /vulnerabilities/csrf/`
**Tool Used:** Burp Suite + Manual

**Issue:** The password change form did not include an anti-CSRF token. A malicious page could silently submit a forged request on behalf of a logged-in user.

**Impact:** An attacker can change a victim's password without their knowledge if they visit a malicious page while logged in.

**Remediation:**
- Implement anti-CSRF tokens on all state-changing forms
- Validate the `Origin` and `Referer` headers server-side
- Use `SameSite=Strict` cookie attribute

---

## Folder Structure
webapp-security-testing-lab/
├── README.md
├── DISCLAIMER.md
├── findings/
│   ├── 01-reflected-xss.md
│   ├── 02-stored-xss.md
│   ├── 03-sql-injection.md
│   └── 04-csrf.md
├── screenshots/
│   ├── xss-payload-fired.png
│   ├── sqli-db-dump.png
│   └── csrf-poc.png
└── remediation-report.md
---

## Key Learnings

- User input should never be trusted — always validate and sanitize both client-side and server-side
- Burp Suite's intercept feature is essential for identifying hidden parameters and request manipulation
- XSS and CSRF are often overlooked but can lead to full account takeover when chained together
- SQL Injection remains one of the most critical vulnerabilities despite being well-known and preventable

---

## References

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [DVWA - Damn Vulnerable Web Application](https://github.com/digininja/DVWA)
- [PortSwigger Web Security Academy](https://portswigger.net/web-security)
- [CWE-79 XSS](https://cwe.mitre.org/data/definitions/79.html)
- [CWE-89 SQL Injection](https://cwe.mitre.org/data/definitions/89.html)

---

## Disclaimer

This project was created for educational purposes only. All testing was performed on intentionally vulnerable applications in an isolated lab environment. Unauthorized testing of any system without explicit permission is illegal and unethical.

---

*Developed by Siva Kumar Kondredy | Cybersecurity *
