# Finding 01 — Reflected XSS

**Severity:** High
**OWASP Category:** A03:2021 — Injection
**CWE:** CWE-79
**Endpoint:** `GET /vulnerabilities/xss_r/?name=`
**Tool Used:** Burp Suite + Manual Testing

---

## Description
The search/name input field reflects user-supplied input directly into the HTML response without any encoding or sanitization, allowing JavaScript to execute in the victim's browser.

## Payload Used
```html
<script>alert('XSS')</script>
```

## Result
Alert box fired in the browser confirming script execution.

## Impact
- Steal session cookies via `document.cookie`
- Redirect users to phishing pages
- Perform actions on behalf of the victim

## Remediation
- Apply HTML entity encoding to all user-supplied output
- Implement Content Security Policy (CSP) headers
- Validate and whitelist input on the server side
