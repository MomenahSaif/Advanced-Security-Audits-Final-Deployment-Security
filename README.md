# Advanced Security Audits & Final Deployment Security

## Overview

This repository documents the completion of advanced security auditing, secure deployment practices, and final penetration testing conducted against OWASP Juice Shop deployed in a Docker-based local environment.

The objective of this project was to:

- Conduct structured security audits
- Evaluate compliance with OWASP Top 10
- Apply secure deployment best practices
- Perform comprehensive manual penetration testing
- Document identified vulnerabilities and applied security controls

Target Application: OWASP Juice Shop  
Deployment Environment: Docker (Localhost)  
Testing Environment: Kali Linux  

---

## Project Structure

```
Advanced-Security-Audits-Final-Deployment-Security/
│
├── 1_Security_Audits/
│   ├── OWASP_ZAP_Report
│   ├── Nikto_Scan_Output
│   ├── Lynis_Audit_Report
│   └── OWASP_Top10_Compliance_Analysis
│
├── 2_Secure_Deployment/
│   ├── Docker_Hardening_Configuration
│   ├── Trivy_Image_Scan
│   └── Deployment_Commands
│
├── 3_Final_Penetration_Testing/
│   ├── Pentest_Report
│   ├── Burp_Testing_Evidence
│   └── Vulnerability_Summary
│
└── screenshots/
```

---

## 1. Security Audits & Compliance

### OWASP ZAP
- Automated web application scan conducted.
- Identified injection flaws, XSS vectors, insecure cookies, and missing security headers.
- Findings mapped to OWASP Top 10 categories.

### Nikto
- Web server configuration audit performed.
- Identified missing HTTP security headers and information disclosure issues.

### Lynis
- Host-level security audit conducted on Kali Linux.
- Evaluated system hardening, services, and configuration weaknesses.
- Recommendations documented for system improvement.

### OWASP Top 10 Compliance Evaluation

The application was assessed against OWASP Top 10 (2021). Due to the intentionally vulnerable nature of Juice Shop, multiple categories were identified as non-compliant, including:

- A01: Broken Access Control
- A02: Cryptographic Failures
- A03: Injection
- A05: Security Misconfiguration
- A06: Vulnerable and Outdated Components

This mapping provides structured risk evaluation rather than remediation of intentionally vulnerable components.

---

## 2. Secure Deployment Practices

### Docker Deployment

- Official OWASP Juice Shop Docker image used.
- Application exposed only on required port (3000).
- No privileged container execution.

### Container Hardening Measures

- `--cap-drop ALL` enforced to remove unnecessary Linux capabilities.
- Verified container not running in privileged mode.
- Docker images regularly updated.
- Unused images pruned to reduce attack surface.

### Vulnerability Scanning

- Container image scanned using Trivy.
- Identified known vulnerabilities in dependencies.
- Results documented to demonstrate dependency risk visibility.

### Host Security

- Automatic security updates enabled on host system.
- System configuration reviewed using Lynis recommendations.

---

## 3. Final Penetration Testing

### Scope

Testing was performed against:
```
http://localhost:3000
```

Environment: Local Docker deployment  
Tool Used: Burp Suite Community Edition  

### Methodology

- Application mapping via Burp Proxy
- Manual request interception and modification
- Parameter manipulation
- HTTP method validation
- Authentication and authorization testing
- Session validation testing

---

## Identified Vulnerabilities

### 1. Broken Access Control (High)

Endpoint:
```
/rest/admin/application-configuration
```

Finding:
Accessible without authentication. The endpoint returned HTTP 200 OK even when no session cookie was provided.

Impact:
Unauthorized exposure of administrative configuration data.

OWASP Category:
A01 – Broken Access Control

---

### 2. Improper Error Handling (Medium)

Endpoint:
```
GET /rest/user/login
```

Finding:
Returned HTTP 500 Internal Server Error instead of HTTP 405 Method Not Allowed.

Impact:
Internal path disclosure and improper method handling.

OWASP Category:
Security Misconfiguration

---

### 3. Proper Session Handling (Positive Observation)

Endpoint:
```
/rest/user/whoami
```

Finding:
Returned empty user object when unauthenticated, demonstrating correct session validation behavior.

---

## Security Improvements Applied

- Docker container executed with least privilege.
- Privileged containers explicitly avoided.
- Container image scanned for known vulnerabilities.
- Host automatic security updates enabled.
- Security audit findings documented and mapped to industry standards.

---

## Key Outcomes

- Structured security audit completed.
- OWASP Top 10 compliance evaluated.
- Secure deployment controls implemented.
- Manual penetration testing performed and documented.
- Vulnerabilities identified with risk classification and remediation guidance.

---

## Disclaimer

OWASP Juice Shop is intentionally designed to be vulnerable for educational purposes.  
All testing was conducted in a controlled local lab environment strictly for cybersecurity training and security auditing practice.
