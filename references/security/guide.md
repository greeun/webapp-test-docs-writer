# Security Test Guide / 보안 테스트 가이드

## Purpose / 목적
Identify and verify security vulnerabilities in web applications.
웹 애플리케이션의 보안 취약점 식별 및 검증.

## Test Targets (OWASP Top 10) / 테스트 대상

| Rank / 순위 | Vulnerability / 취약점 | Description / 설명 |
|-------------|------------------------|-------------------|
| A01 | Broken Access Control | Access bypass / 권한 우회 |
| A02 | Cryptographic Failures | Encryption failures / 암호화 실패 |
| A03 | Injection | SQL/NoSQL/Command Injection |
| A04 | Insecure Design | Security design flaws / 보안 설계 미흡 |
| A05 | Security Misconfiguration | Security config errors / 보안 설정 오류 |
| A06 | Vulnerable Components | Vulnerable libraries / 취약한 라이브러리 |
| A07 | Auth Failures | Authentication failures / 인증 실패 |
| A08 | Data Integrity Failures | Data integrity issues / 데이터 무결성 |
| A09 | Logging Failures | Missing logs / 로깅 부재 |
| A10 | SSRF | Server-Side Request Forgery |

## Scenario Derivation Criteria / 시나리오 도출 기준

### 1. Authentication / 인증
| Scenario / 시나리오 | Test Content / 테스트 내용 |
|---------------------|---------------------------|
| Brute force / 브루트포스 | Account lockout after multiple attempts / 다수 로그인 시도 시 잠금 |
| Session management / 세션 관리 | Session fixation, expiry, hijacking / 세션 고정, 만료, 탈취 |
| Password policy / 비밀번호 정책 | Complexity, history management / 복잡도, 이력 관리 |
| MFA | MFA bypass attempts / 다중 인증 우회 시도 |

### 2. Authorization / 인가
| Scenario / 시나리오 | Test Content / 테스트 내용 |
|---------------------|---------------------------|
| Horizontal privilege escalation / 수평 권한 상승 | Access other user's data / 다른 사용자 데이터 접근 |
| Vertical privilege escalation / 수직 권한 상승 | Access admin functions / 관리자 기능 접근 |
| IDOR | Insecure direct object reference / 직접 객체 참조 취약점 |
| Function-level access / 기능 수준 접근 | Hidden API endpoints / 숨겨진 API 엔드포인트 |

### 3. Input Validation / 입력 검증
| Attack Type / 공격 유형 | Test Payload / 테스트 페이로드 |
|------------------------|------------------------------|
| XSS | `<script>alert(1)</script>` |
| SQL Injection | `' OR '1'='1` |
| Command Injection | `; ls -la` |
| Path Traversal | `../../../etc/passwd` |

### 4. Data Protection / 데이터 보호
- HTTPS enforcement / HTTPS 강제 여부
- Sensitive data masking / 민감 데이터 마스킹
- Token/API key exposure / 토큰/API키 노출
- Error message information leak / 에러 메시지 정보 노출

## Test Case Example / 테스트 케이스 예시

```markdown
## TC-SEC-001: SQL Injection - Login form / 로그인 폼

| Item / 항목 | Content / 내용 |
|-------------|----------------|
| **Vulnerability / 취약점** | A03 - Injection |
| **Priority / 우선순위** | Critical |

### Test Data / 테스트 데이터
| Input Field / 입력 필드 | Payload / 페이로드 |
|-------------------------|-------------------|
| username | `admin'--` |
| username | `' OR '1'='1` |
| password | `' OR '1'='1'--` |

### Test Steps / 테스트 단계
| # | Step / 단계 | Expected Result / 예상 결과 |
|---|-------------|----------------------------|
| 1 | Login attempt with payload / 페이로드 입력 후 로그인 시도 | Login fails / 로그인 실패 |
| 2 | Check error response / 에러 응답 확인 | No SQL error exposed / SQL 에러 노출 없음 |
| 3 | Check server logs / 서버 로그 확인 | Attack attempt logged / 공격 시도 기록됨 |

### Pass Criteria / 통과 기준
- All payloads result in auth failure / 모든 페이로드에서 인증 실패
- No SQL error message exposed / SQL 에러 메시지 미노출
- Security logs recorded / 보안 로그 기록
```

## Automation Tools / 자동화 도구
- OWASP ZAP
- Burp Suite
- sqlmap
- nikto
- Snyk, Dependabot (dependencies / 의존성)
