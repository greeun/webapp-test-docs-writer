# Security Test Guide

## Purpose
Identify and verify security vulnerabilities in web applications.

## Test Targets (OWASP Top 10)

| Rank | Vulnerability | Description |
|------|---------------|-------------|
| A01 | Broken Access Control | Access bypass |
| A02 | Cryptographic Failures | Encryption failures |
| A03 | Injection | SQL/NoSQL/Command Injection |
| A04 | Insecure Design | Security design flaws |
| A05 | Security Misconfiguration | Security config errors |
| A06 | Vulnerable Components | Vulnerable libraries |
| A07 | Auth Failures | Authentication failures |
| A08 | Data Integrity Failures | Data integrity issues |
| A09 | Logging Failures | Missing logs |
| A10 | SSRF | Server-Side Request Forgery |

## Scenario Derivation Criteria

### 1. Authentication
| Scenario | Test Content |
|----------|--------------|
| Brute force | Account lockout after multiple attempts |
| Session management | Session fixation, expiry, hijacking |
| Password policy | Complexity, history management |
| MFA | MFA bypass attempts |

### 2. Authorization
| Scenario | Test Content |
|----------|--------------|
| Horizontal privilege escalation | Access other user's data |
| Vertical privilege escalation | Access admin functions |
| IDOR | Insecure direct object reference |
| Function-level access | Hidden API endpoints |

### 3. Input Validation
| Attack Type | Test Payload |
|-------------|--------------|
| XSS | `<script>alert(1)</script>` |
| SQL Injection | `' OR '1'='1` |
| Command Injection | `; ls -la` |
| Path Traversal | `../../../etc/passwd` |

### 4. Data Protection
- HTTPS enforcement
- Sensitive data masking
- Token/API key exposure
- Error message information leak

## Test Case Example

```markdown
## TC-SEC-001: SQL Injection - Login form

| Item | Content |
|------|---------|
| **Vulnerability** | A03 - Injection |
| **Priority** | Critical |

### Test Data
| Input Field | Payload |
|-------------|---------|
| username | `admin'--` |
| username | `' OR '1'='1` |
| password | `' OR '1'='1'--` |

### Test Steps
| # | Step | Expected Result |
|---|------|-----------------|
| 1 | Login attempt with payload | Login fails |
| 2 | Check error response | No SQL error exposed |
| 3 | Check server logs | Attack attempt logged |

### Pass Criteria
- All payloads result in auth failure
- No SQL error message exposed
- Security logs recorded
```

## Automation Tools
- OWASP ZAP
- Burp Suite
- sqlmap
- nikto
- Snyk, Dependabot (dependencies)
