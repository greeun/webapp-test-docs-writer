# Unit Test Guide / 단위 테스트 가이드

## Purpose / 목적
Verify individual functions, methods, and modules in isolation.
개별 함수, 메서드, 모듈을 격리된 환경에서 검증.

## Test Targets / 테스트 대상
- Pure functions (business logic) / 순수 함수 (비즈니스 로직)
- Utility functions / 유틸리티 함수
- Data transformation/parsing / 데이터 변환/파싱
- State management (reducers, stores) / 상태 관리 (리듀서, 스토어)
- Custom hooks (React) / 커스텀 훅
- Class methods / 클래스 메서드

## Scenario Derivation Criteria / 시나리오 도출 기준

### 1. Input-based / 입력 기반
| Category / 구분 | Test Case / 테스트 케이스 |
|-----------------|-------------------------|
| Valid input / 정상 입력 | Normal operation with valid values / 유효한 값으로 정상 동작 |
| Boundary values / 경계값 | Min, max, boundary conditions / 최소값, 최대값, 경계 조건 |
| Invalid input / 잘못된 입력 | null, undefined, empty, wrong type / null, undefined, 빈값, 잘못된 타입 |
| Special cases / 특수 케이스 | Empty array, empty object, special chars / 빈 배열, 빈 객체, 특수문자 |

### 2. Branch-based / 분기 기반
- Cover all if/else branches / 모든 if/else 분기 커버
- All switch cases / switch 문의 모든 case
- Both sides of ternary operators / 삼항 연산자 양쪽 결과
- Early return conditions / 조기 반환 (early return) 조건

### 3. Exception-based / 예외 기반
- All thrown exceptions / throw하는 모든 예외 상황
- catch paths in try-catch / try-catch 블록의 catch 경로
- Error message accuracy / 에러 메시지 정확성

## Test Case Example / 테스트 케이스 예시

```markdown
## TC-UNIT-001: calculateTotal - Normal calculation / 정상 계산

| Item / 항목 | Content / 내용 |
|-------------|----------------|
| **Target / 대상** | `calculateTotal(items)` |
| **Priority / 우선순위** | High |

### Test Data / 테스트 데이터
| Input / 입력 | Expected Output / 예상 출력 |
|--------------|----------------------------|
| `[{price: 100, qty: 2}]` | `200` |
| `[{price: 100, qty: 2}, {price: 50, qty: 1}]` | `250` |

### Verification / 검증
- Return value is number type / 반환값이 숫자 타입인가
- Calculation is accurate / 계산이 정확한가
```

## Coverage Goals / 커버리지 목표

| Metric / 메트릭 | Target / 목표 |
|-----------------|---------------|
| Line Coverage | >= 80% |
| Branch Coverage | >= 75% |
| Function Coverage | >= 90% |

## Automation Tools / 자동화 도구
- JavaScript/TypeScript: Jest, Vitest
- Python: pytest
- Go: testing
- Java: JUnit
