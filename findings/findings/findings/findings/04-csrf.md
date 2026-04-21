# Finding 04 — CSRF (Cross-Site Request Forgery)

**Severity:** Medium
**OWASP Category:** A01:2021 — Broken Access Control
**CWE:** CWE-352
**Endpoint:** `POST /vulnerabilities/csrf/`
**Tool Used:** Burp Suite + Manual Testing

---

## Description
The password change form does not include an anti-CSRF token. A logged-in user can be tricked into submitting a forged request from a malicious third-party page, silently changing their password.

## How It Was Identified
Intercepted the password change request in Burp Suite — confirmed no CSRF token present in the form or request headers.

## Proof of Concept
A malicious HTML page with an auto-submitting form targeting the endpoint would silently change the victim's password if they are logged in and visit the page.

## Impact
- Attacker can change victim's password without their knowledge
- Full account takeover once password is changed
- No user interaction beyond visiting a malicious page required

## Remediation
- Implement anti-CSRF tokens on all state-changing forms
- Validate `Origin` and `Referer` headers server-side
- Set `SameSite=Strict` on session cookies
- Require re-authentication for sensitive actions like password changes
