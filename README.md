# Task 3: API Security Risk Analysis

Part of the Future Interns Cyber Security Internship — Yuvraj Singh (CEH v13)

## Target
`https://jsonplaceholder.typicode.com` — public REST API test sandbox

## Scope
Manual black-box testing performed with Postman. No exploitation, DoS, or
destructive actions were performed; all requests used the API's own
documented endpoints and standard HTTP methods.

## Methodology
1. Reconnaissance of available endpoints
2. Authentication check on `GET /users`
3. Object-level authorization check via `GET /users/{id}` (BOLA/IDOR test)
4. Boundary testing (`GET /users/26` — out-of-range ID)
5. Response header review for missing security controls
6. `POST /posts` tested with valid and malformed/malicious payloads
   (empty body, wrong data types, oversized strings, script tags)
7. Verified authentication configuration via Postman's Authorization tab

## Findings summary

| # | Finding | Severity |
|---|---|---|
| 1 | No authentication on `GET /users` (PII exposure) | High |
| 2 | BOLA/IDOR on `GET /users/{id}` | Medium–High |
| 3 | No authentication on `POST /posts` (write access) | High (context-dependent) |
| 4 | Verbose error disclosure — 500 error exposes Node.js stack trace | Medium–High |
| 5 | Insufficient input validation | Medium |
| 6 | Missing `X-Frame-Options` / `Content-Security-Policy` headers | Low |

Full details, evidence references, and remediation recommendations are in
`/report/Task3_API_Security_Risk_Analysis.pdf`.

## Evidence
See `/evidence` for annotated screenshots supporting each finding.

## Tools used
Postman

## Disclaimer
Testing was conducted against a public test/demo API intended for practice
purposes (jsonplaceholder.typicode.com), not a production system.
