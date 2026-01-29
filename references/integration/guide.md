# Integration Test Guide / 통합 테스트 가이드

## Purpose / 목적
Verify that multiple components/modules work correctly together.
여러 컴포넌트/모듈이 함께 올바르게 동작하는지 검증.

## Test Targets / 테스트 대상
- Service layer ↔ Database / 서비스 레이어 ↔ 데이터베이스
- Component ↔ API client / 컴포넌트 ↔ API 클라이언트
- State management ↔ UI component / 상태 관리 ↔ UI 컴포넌트
- External service integration / 외부 서비스 연동
- Event publish/subscribe / 이벤트 발행/구독

## Scenario Derivation Criteria / 시나리오 도출 기준

### 1. Data Flow / 데이터 흐름
| Category / 구분 | Verification Point / 검증 포인트 |
|-----------------|--------------------------------|
| Input → Process → Save / 입력 → 처리 → 저장 | Data integrity / 데이터 정합성 |
| Query → Transform → Output / 조회 → 변환 → 출력 | Data consistency / 데이터 일관성 |
| Event publish → Subscribe → Process / 이벤트 발행 → 구독 → 처리 | Event delivery / 이벤트 전달 |

### 2. State Changes / 상태 변화
- Initial state → Action → Changed state / 초기 상태 → 액션 → 변경된 상태
- Chained state changes (A → B → C) / 연쇄 상태 변화
- State recovery on rollback/failure / 롤백/실패 시 상태 복구

### 3. Transactions / 트랜잭션
- Commit on success / 성공 시 커밋
- Rollback on failure / 실패 시 롤백
- Partial failure handling / 부분 실패 처리

## Test Case Example / 테스트 케이스 예시

```markdown
## TC-INT-001: User creation and retrieval / 사용자 생성 및 조회

| Item / 항목 | Content / 내용 |
|-------------|----------------|
| **Scope / 범위** | UserService ↔ UserRepository ↔ Database |
| **Priority / 우선순위** | Critical |

### Preconditions / 전제조건
- Test DB connected / 테스트 DB 연결
- users table is empty / users 테이블 비어있음

### Test Steps / 테스트 단계
| # | Step / 단계 | Expected Result / 예상 결과 |
|---|-------------|----------------------------|
| 1 | Call `userService.create({name: "Kim"})` / 호출 | Returns created user object / 생성된 user 객체 반환 |
| 2 | Call `userService.findById(id)` / 호출 | Returns same user / 동일한 user 조회 |
| 3 | Direct DB query / DB에서 직접 조회 | Record exists / 레코드 존재 확인 |

### Cleanup / 정리
- Delete created test data / 생성된 테스트 데이터 삭제
```

## Test Environment / 테스트 환경

| Environment / 환경 | Description / 설명 |
|--------------------|-------------------|
| **Test DB / 테스트 DB** | Use dedicated test DB / 별도 테스트 전용 DB 사용 |
| **Mock Server** | Mock external APIs / 외부 API는 Mock 처리 |
| **Isolation / 격리** | Data isolation between tests / 각 테스트 간 데이터 격리 |

## Automation Tools / 자동화 도구
- Jest + Supertest (Node.js)
- pytest + TestClient (Python/FastAPI)
- Spring Boot Test (Java)
- Testcontainers (Docker-based / Docker 기반)
