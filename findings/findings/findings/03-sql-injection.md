# Finding 03 — SQL Injection

**Severity:** Critical
**OWASP Category:** A03:2021 — Injection
**CWE:** CWE-89
**Endpoint:** `POST /vulnerabilities/sqli/`
**Tool Used:** Burp Suite + Manual Testing

---

## Description
The user ID input field is directly concatenated into a SQL query without parameterization or sanitization, allowing an attacker to manipulate the query logic and extract database contents.

## Payload Used
```sql
' OR '1'='1
```

## Result
Application returned all user records from the database including usernames and password hashes, bypassing intended query logic.

## Impact
- Full database extraction including credentials
- Authentication bypass
- Data modification or deletion
- In severe cases, remote code execution via database features

## Remediation
- Use parameterized queries / prepared statements exclusively
- Never concatenate user input directly into SQL strings
- Apply least privilege to database accounts
- Use a Web Application Firewall (WAF) as an additional layer
