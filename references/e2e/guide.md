# E2E Test Guide / E2E 테스트 가이드

## Purpose / 목적
Verify complete system flows from the real user's perspective.
실제 사용자 관점에서 전체 시스템 흐름 검증.

## Test Targets / 테스트 대상
- Core user scenarios / 핵심 사용자 시나리오
- Page navigation / 페이지 간 네비게이션
- Form input and submission / 폼 입력 및 제출
- Auth flow (login/logout) / 인증 흐름 (로그인/로그아웃)
- Core business flows (payment, order) / 결제/주문 등 핵심 비즈니스 플로우

## Scenario Derivation Criteria / 시나리오 도출 기준

### 1. User Journey / 사용자 여정
| Category / 구분 | Example / 예시 |
|-----------------|----------------|
| New user / 신규 사용자 | Sign up → Email verification → Profile setup / 회원가입 → 이메일 인증 → 프로필 설정 |
| Buyer / 구매자 | Search → Select product → Cart → Checkout / 검색 → 상품 선택 → 장바구니 → 결제 |
| Admin / 관리자 | Login → Dashboard → View/Edit data / 로그인 → 대시보드 → 데이터 조회/수정 |

### 2. Core Function Flows / 핵심 기능 흐름
- Login → Main → Use feature → Logout / 로그인 → 메인 → 기능 사용 → 로그아웃
- Error occurs → Error page → Recovery / 에러 발생 → 에러 페이지 → 복구
- Session expired → Re-login → Restore state / 세션 만료 → 재로그인 → 이전 상태 복원

### 3. Cross Browser/Device / 크로스 브라우저/디바이스
- Chrome, Firefox, Safari
- Desktop, Tablet, Mobile
- Responsive layout / 반응형 레이아웃

## Test Case Example / 테스트 케이스 예시

```markdown
## TC-E2E-001: Complete sign-up flow / 회원가입 전체 흐름

| Item / 항목 | Content / 내용 |
|-------------|----------------|
| **Scenario / 시나리오** | New user completes sign-up / 신규 사용자 회원가입 완료 |
| **Priority / 우선순위** | Critical |
| **Expected Duration / 예상 소요** | 2 min / 2분 |

### Preconditions / 전제조건
- Test email available / 테스트 이메일 사용 가능
- Browser: Chrome latest / 브라우저: Chrome 최신

### Test Steps / 테스트 단계
| # | Page / 페이지 | Action / 액션 | Expected Result / 예상 결과 |
|---|---------------|---------------|----------------------------|
| 1 | Home / 홈 | Click "Sign Up" / "회원가입" 클릭 | Sign-up form displayed / 회원가입 폼 표시 |
| 2 | Sign Up / 회원가입 | Enter email / 이메일 입력 | Validation passes / 유효성 통과 |
| 3 | Sign Up / 회원가입 | Enter password / 비밀번호 입력 | Strength indicator / 강도 표시 |
| 4 | Sign Up / 회원가입 | Click "Sign Up" button / "가입" 버튼 클릭 | Verification email notice / 인증 메일 안내 |
| 5 | Email / 이메일 | Click verification link / 인증 링크 클릭 | Completion page / 가입 완료 페이지 |
| 6 | Complete / 완료 | Auto-login / 자동 로그인 | Main page, username displayed / 메인 페이지, 사용자명 표시 |

### Verification / 검증
- [ ] URL changes at each step / 각 단계에서 URL 변경 확인
- [ ] No error messages / 에러 메시지 없음
- [ ] User created in DB / DB에 사용자 생성됨
```

## Test Design Principles / 테스트 설계 원칙

| Principle / 원칙 | Description / 설명 |
|------------------|-------------------|
| **Independence / 독립성** | Each test can run independently / 각 테스트는 독립 실행 가능 |
| **Repeatability / 반복성** | Same results can be reproduced / 동일 결과 재현 가능 |
| **Stability / 안정성** | Minimize flaky tests / Flaky 테스트 최소화 |
| **Readability / 가독성** | Clear intent in steps / 의도가 명확한 단계 |

## Automation Tools / 자동화 도구
- Playwright (Recommended / 권장)
- Cypress
- Selenium WebDriver
- Puppeteer
