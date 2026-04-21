# Finding 02 — Stored XSS

**Severity:** High
**OWASP Category:** A03:2021 — Injection
**CWE:** CWE-79
**Endpoint:** `POST /vulnerabilities/xss_s/`
**Tool Used:** Burp Suite + Manual Testing

---

## Description
The message/comment input field stores user-supplied data in the database and renders it back to all users without sanitization. Any JavaScript payload stored is executed in every visitor's browser.

## Payload Used
```html
<script>alert('Stored XSS')</script>
```

## Result
Every user who visits the page triggers the script automatically — confirmed with alert box firing on page load.

## Impact
- Persistent attack affecting all users, not just one
- Mass session cookie theft
- Defacement or malicious redirects for every visitor

## Remediation
- Sanitize and encode data before storing it in the database
- Encode output at the point of rendering
- Use a Content Security Policy (CSP) to block inline scripts
