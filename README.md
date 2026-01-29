# webapp-test-docs-writer

Web Service Test Documentation Writer Skill for Claude Code.
웹서비스 테스트 문서 작성 스킬.

## Overview / 개요

This skill generates test scenarios and test cases for web service verification. It supports 7 test types and outputs bilingual (English/Korean) documentation.

이 스킬은 웹서비스 검증을 위한 테스트 시나리오와 테스트 케이스를 생성합니다. 7가지 테스트 유형을 지원하며 영어/한글 이중 언어 문서를 출력합니다.

## Installation / 설치

### Option 1: Symlink (Development)

```bash
# Clone or copy the skill folder
ln -s /path/to/webapp-test-docs-writer ~/.claude/skills/webapp-test-docs-writer
```

### Option 2: From .skill Package

```bash
# Copy .skill file and extract
cp webapp-test-docs-writer.skill ~/.claude/skills/
cd ~/.claude/skills/
unzip webapp-test-docs-writer.skill -d webapp-test-docs-writer
rm webapp-test-docs-writer.skill
```

## Usage / 사용법

### Trigger Keywords / 트리거 키워드

| Language | Keywords |
|----------|----------|
| **English** | "test case", "test scenario", "write tests", "QA documentation" |
| **한글** | "테스트 케이스 작성", "테스트 시나리오", "QA 문서" |

### Example Prompts / 예시 프롬프트

```
# English
"Write test cases for the login feature"
"Create API test scenarios for user registration"
"Generate E2E test cases for checkout flow"
"Write security test cases for authentication"

# 한글
"로그인 기능 테스트 케이스 작성해줘"
"회원가입 API 테스트 시나리오 만들어줘"
"결제 흐름 E2E 테스트 케이스 생성해줘"
"인증 보안 테스트 케이스 작성해줘"
```

## Test Types / 테스트 유형

| Type | Purpose | Guide |
|------|---------|-------|
| **Unit** | Individual function/module verification | `references/unit/guide.md` |
| **Integration** | Component interaction verification | `references/integration/guide.md` |
| **API** | REST/GraphQL endpoint verification | `references/api/guide.md` |
| **E2E** | Complete user flow verification | `references/e2e/guide.md` |
| **Security** | Security vulnerability verification | `references/security/guide.md` |
| **Performance** | Performance/load verification | `references/performance/guide.md` |
| **Accessibility** | WCAG compliance verification | `references/accessibility/guide.md` |

## Workflow / 워크플로우

```
1. Analyze Input    → 2. Select Test Type → 3. Derive Scenarios → 4. Write Cases → 5. Review
   입력 분석           테스트 유형 선택       시나리오 도출         케이스 작성       리뷰
```

### Step 1: Analyze Input / 입력 분석

The skill analyzes these sources:
- Functional specifications / 기능 명세서
- API specifications (OpenAPI/Swagger)
- Source code analysis / 소스 코드 분석

### Step 2: Select Test Type / 테스트 유형 선택

Choose appropriate test type based on the feature being tested.

### Step 3: Derive Scenarios / 시나리오 도출

Scenarios are derived from 4 perspectives:
1. **Happy Path** - Expected normal behavior
2. **Alternative** - Success via different path
3. **Exception** - Error/failure cases
4. **Boundary** - Min/max/edge conditions

### Step 4: Write Cases / 케이스 작성

Each test case includes:
- ID (e.g., TC-API-001)
- Title / 제목
- Preconditions / 전제조건
- Test Steps / 테스트 단계
- Expected Results / 예상 결과
- Priority / 우선순위
- Test Data / 테스트 데이터
- Automation feasibility / 자동화 가능성

### Step 5: Review / 리뷰

Checklist:
- [ ] 100% requirements coverage
- [ ] Both positive/negative cases included
- [ ] Boundary tests included
- [ ] Test data is clear
- [ ] Steps are reproducible
- [ ] Expected results are verifiable

## Output Format / 출력 형식

### Deliverables / 산출물

| # | Document | Format | Description |
|---|----------|--------|-------------|
| 1 | Test Scenario Document | Markdown | Scenario list with coverage |
| 2 | Test Case Document | Markdown Table | Detailed test steps |
| 3 | Coverage Matrix | Markdown Table | Requirement-Scenario-Case mapping |

### Scenario vs Test Case / 시나리오 vs 케이스

| Criteria | Scenario | Test Case |
|----------|----------|-----------|
| **Level** | High (What to test) | Low (How to test) |
| **Perspective** | Business/User | Technical/Executor |
| **Detail** | Overview | Specific steps |
| **Relation** | 1 Scenario = N Cases | N Cases ⊂ 1 Scenario |

### ID Naming Convention / ID 명명 규칙

```
Scenario: SC-[FEATURE]-[NNN]
Example: SC-LOGIN-001, SC-PAYMENT-003

Test Case: TC-[TYPE]-[NNN] or TC-[FEATURE]-[NNN]
Example: TC-API-001, TC-E2E-015, TC-LOGIN-007

TYPE codes:
- UNIT: Unit test
- INT: Integration test
- API: API test
- E2E: E2E test
- SEC: Security test
- PERF: Performance test
- A11Y: Accessibility test
```

### Priority Levels / 우선순위

| Priority | Criteria | Example |
|----------|----------|---------|
| **Critical** | Core business, service unavailable if fails | Login, Payment |
| **High** | Major function, significant UX impact | Search, Order |
| **Medium** | Supporting function, alternative exists | Filter, Sort |
| **Low** | Additional function, minimal impact | UI enhancement |

## Sample Output / 출력 예시

### Test Scenario Document

```markdown
# 로그인 기능 테스트 시나리오

## 개요
| 항목 | 내용 |
|------|------|
| **테스트 대상** | 사용자 인증 시스템 |
| **테스트 범위** | 로그인, 소셜 로그인, 계정 잠금 |
| **테스트 유형** | API, E2E |

## 시나리오 목록

| ID | 시나리오 | 흐름 유형 | 우선순위 | 케이스 수 |
|----|----------|----------|----------|----------|
| SC-LOGIN-001 | 유효한 자격증명으로 로그인 | Happy Path | Critical | 3 |
| SC-LOGIN-002 | 잘못된 자격증명으로 실패 | Exception | High | 4 |
```

### Test Case Document

```markdown
## TC-API-001: 이메일+비밀번호 정상 로그인

| 항목 | 내용 |
|------|------|
| **우선순위** | Critical |
| **전제조건** | - 유효한 계정 존재<br>- 로그아웃 상태 |
| **테스트 데이터** | `{"email": "test@example.com", "password": "Pass123!"}` |

### 테스트 단계

| # | 단계 | 예상 결과 |
|---|------|----------|
| 1 | POST /api/auth/login 호출 | 200 OK |
| 2 | 응답 body 확인 | accessToken 포함 |

### 메타 정보
- 자동화: 가능 (Jest + Supertest)
- 관련 요구사항: REQ-AUTH-001
```

## File Structure / 파일 구조

```
webapp-test-docs-writer/
├── SKILL.md                          # Main skill definition
├── README.md                         # This file
├── webapp-test-docs-writer.skill     # Packaged skill (zip)
└── references/
    ├── templates.md                  # Common templates
    ├── unit/guide.md                 # Unit test guide
    ├── integration/guide.md          # Integration test guide
    ├── api/guide.md                  # API test guide
    ├── e2e/guide.md                  # E2E test guide
    ├── security/guide.md             # Security test guide
    ├── performance/guide.md          # Performance test guide
    └── accessibility/guide.md        # Accessibility test guide
```

## Automation Tools Reference / 자동화 도구 참조

| Test Type | Tools |
|-----------|-------|
| **Unit** | Jest, Vitest, pytest, JUnit |
| **Integration** | Supertest, TestClient, Spring Boot Test |
| **API** | Postman/Newman, REST Assured, httpx |
| **E2E** | Playwright, Cypress, Selenium |
| **Security** | OWASP ZAP, Burp Suite, sqlmap |
| **Performance** | k6, JMeter, Gatling, Locust |
| **Accessibility** | axe DevTools, WAVE, Lighthouse |

## License

MIT License

## Author

Created with Claude Code skill-wizard.
