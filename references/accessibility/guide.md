# Accessibility Test Guide / 접근성 테스트 가이드

## Purpose / 목적
Ensure WCAG 2.1 compliance and accessibility for all users.
WCAG 2.1 가이드라인 준수 및 모든 사용자의 접근성 보장.

## WCAG Principles (POUR) / WCAG 원칙

| Principle / 원칙 | Description / 설명 | Example / 예시 |
|------------------|-------------------|----------------|
| **Perceivable** | Can be perceived / 인지 가능 | Alt text, captions / 대체 텍스트, 자막 |
| **Operable** | Can be operated / 조작 가능 | Keyboard access, sufficient time / 키보드 접근, 충분한 시간 |
| **Understandable** | Can be understood / 이해 가능 | Clear labels, error guidance / 명확한 라벨, 에러 안내 |
| **Robust** | Robust / 견고함 | Assistive technology compatible / 보조 기술 호환 |

## Scenario Derivation Criteria / 시나리오 도출 기준

### 1. Visual Accessibility / 시각 접근성
| Item / 항목 | Test Content / 테스트 내용 | WCAG |
|-------------|---------------------------|------|
| Alt text / 대체 텍스트 | Images have alt attribute / 이미지에 alt 속성 | 1.1.1 |
| Contrast / 명암비 | Text 4.5:1 or higher / 텍스트 4.5:1 이상 | 1.4.3 |
| Text size / 텍스트 크기 | Usable at 200% zoom / 200% 확대 시 사용 가능 | 1.4.4 |
| Color dependence / 색상 의존 | No info conveyed by color alone / 색상만으로 정보 전달 X | 1.4.1 |

### 2. Keyboard Accessibility / 키보드 접근성
| Item / 항목 | Test Content / 테스트 내용 | WCAG |
|-------------|---------------------------|------|
| Keyboard navigation / 키보드 탐색 | Tab reaches all elements / Tab으로 모든 요소 접근 | 2.1.1 |
| Focus indicator / 포커스 표시 | Visual indication of current position / 현재 위치 시각적 표시 | 2.4.7 |
| Keyboard trap / 키보드 트랩 | Not trapped in any element / 특정 요소에 갇히지 않음 | 2.1.2 |
| Shortcuts / 단축키 | No conflicting shortcuts / 충돌 없는 단축키 | 2.1.4 |

### 3. Screen Reader Compatibility / 스크린리더 호환
| Item / 항목 | Test Content / 테스트 내용 | WCAG |
|-------------|---------------------------|------|
| Semantic markup / 시맨틱 마크업 | Correct HTML elements used / 올바른 HTML 요소 사용 | 1.3.1 |
| Landmarks / 랜드마크 | main, nav, header, etc. | 1.3.1 |
| Form labels / 폼 라벨 | input and label connected / input과 label 연결 | 1.3.1 |
| Dynamic content / 동적 콘텐츠 | aria-live announcements / aria-live로 알림 | 4.1.3 |

### 4. Cognitive Accessibility / 인지 접근성
| Item / 항목 | Test Content / 테스트 내용 | WCAG |
|-------------|---------------------------|------|
| Error messages / 에러 메시지 | Clear error description / 명확한 오류 설명 | 3.3.1 |
| Input hints / 입력 힌트 | Expected format guidance / 예상 형식 안내 | 3.3.2 |
| Consistent navigation / 일관된 탐색 | Same menu structure / 동일한 메뉴 구조 | 3.2.3 |
| Sufficient time / 충분한 시간 | Timeout extension option / 타임아웃 연장 옵션 | 2.2.1 |

## Test Case Example / 테스트 케이스 예시

```markdown
## TC-A11Y-001: Login form keyboard accessibility / 로그인 폼 키보드 접근성

| Item / 항목 | Content / 내용 |
|-------------|----------------|
| **WCAG** | 2.1.1 (Keyboard) |
| **Priority / 우선순위** | High |

### Preconditions / 전제조건
- No mouse used / 마우스 미사용
- Screen reader enabled (VoiceOver/NVDA) / 스크린리더 활성화

### Test Steps / 테스트 단계
| # | Step / 단계 | Expected Result / 예상 결과 |
|---|-------------|----------------------------|
| 1 | Tab to email field / Tab으로 이메일 필드 이동 | Focus visible, label read / 포커스 표시, 라벨 읽음 |
| 2 | Enter email / 이메일 입력 | Input possible / 입력 가능 |
| 3 | Tab to password / Tab으로 비밀번호 이동 | Focus visible, label read / 포커스 표시, 라벨 읽음 |
| 4 | Submit with Enter / Enter로 폼 제출 | Login executes / 로그인 실행 |
| 5 | On error / 에러 시 | Error message auto-read / 에러 메시지 자동 읽음 |

### Verification / 검증
- [ ] All elements accessible via Tab / 모든 요소 Tab 접근 가능
- [ ] Focus visually indicated / 포커스 시각적 표시
- [ ] Screen reader labels accurate / 스크린리더 라벨 정확
- [ ] Form submittable via keyboard / 폼 제출 키보드로 가능
```

## Test Tools / 테스트 도구

| Tool / 도구 | Purpose / 용도 |
|-------------|----------------|
| **axe DevTools** | Automated testing / 자동 검사 |
| **WAVE** | Web accessibility evaluation / 웹 접근성 평가 |
| **Lighthouse** | Accessibility score / 접근성 점수 |
| **VoiceOver** | macOS screen reader / macOS 스크린리더 |
| **NVDA** | Windows screen reader / Windows 스크린리더 |
| **Color Contrast Analyzer** | Contrast check / 명암비 검사 |

## Compliance Levels / 준수 레벨

| Level / 레벨 | Description / 설명 |
|--------------|-------------------|
| **A** | Minimum requirements / 최소 요구사항 |
| **AA** | Recommended (legal standard) / 권장 (법적 기준) |
| **AAA** | Highest level / 최고 수준 |

Target / 목표: **WCAG 2.1 Level AA** compliance / 준수
