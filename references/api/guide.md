# API Test Guide / API 테스트 가이드

## Purpose / 목적
Verify correct operation of REST/GraphQL API endpoints.
REST/GraphQL API 엔드포인트의 정확한 동작 검증.

## Test Targets / 테스트 대상
- HTTP methods (GET, POST, PUT, DELETE, PATCH) / HTTP 메서드
- Request parameters (path, query, body, header) / 요청 파라미터
- Response (status code, body, header) / 응답
- Authentication/Authorization / 인증/인가
- Error responses / 에러 응답

## Scenario Derivation Criteria / 시나리오 도출 기준

### 1. CRUD Basics / CRUD 기본
| Operation / 작업 | Test Cases / 테스트 케이스 |
|------------------|--------------------------|
| Create | Normal creation, missing required fields, duplicate data / 정상 생성, 필수값 누락, 중복 데이터 |
| Read | Existing resource, non-existing resource, list query / 존재하는 리소스, 없는 리소스, 목록 조회 |
| Update | Full update, partial update, update non-existing / 전체 수정, 부분 수정, 없는 리소스 수정 |
| Delete | Normal delete, delete non-existing, related data / 정상 삭제, 없는 리소스 삭제, 연관 데이터 |

### 2. Status Codes / 상태 코드
| Code / 코드 | Scenario / 시나리오 |
|-------------|---------------------|
| 200 | Success response / 정상 응답 |
| 201 | Resource created / 리소스 생성 |
| 204 | No content (delete) / 내용 없음 (삭제) |
| 400 | Bad request / 잘못된 요청 |
| 401 | Authentication failed / 인증 실패 |
| 403 | Forbidden / 권한 없음 |
| 404 | Resource not found / 리소스 없음 |
| 409 | Conflict (duplicate) / 충돌 (중복) |
| 422 | Validation failed / 유효성 검사 실패 |
| 500 | Server error / 서버 오류 |

### 3. Authentication/Authorization / 인증/인가
- Request without token / 토큰 없이 요청
- Expired token / 만료된 토큰
- Unauthorized user / 권한 없는 사용자
- Role-based access control / 역할별 접근 제어

### 4. Paging/Sorting/Filtering / 페이징/정렬/필터
- Default paging / 기본 페이징
- Custom page size / 커스텀 page size
- Sort options / 정렬 옵션
- Complex filters / 복합 필터

## Test Case Example / 테스트 케이스 예시

```markdown
## TC-API-001: Get user list / 사용자 목록 조회

| Item / 항목 | Content / 내용 |
|-------------|----------------|
| **Endpoint / 엔드포인트** | `GET /api/v1/users` |
| **Priority / 우선순위** | High |

### Request / 요청
| Item / 항목 | Value / 값 |
|-------------|------------|
| Method | GET |
| Headers | `Authorization: Bearer {token}` |
| Query | `page=1&limit=10&sort=createdAt:desc` |

### Test Cases / 테스트 케이스
| # | Scenario / 시나리오 | Expected Status / 예상 상태 | Verification / 검증 |
|---|---------------------|----------------------------|---------------------|
| 1 | Normal request / 정상 요청 | 200 | Returns array, pagination info / 배열 반환, pagination 정보 |
| 2 | No token / 토큰 없음 | 401 | error message |
| 3 | Invalid page / 잘못된 page | 400 | validation error |
```

## Response Verification Points / 응답 검증 포인트

| Item / 항목 | Verification / 검증 내용 |
|-------------|-------------------------|
| **Status Code** | Matches expected code / 예상 코드와 일치 |
| **Response Time** | Within SLA / SLA 내 응답 |
| **Body Schema** | Schema match (JSON Schema) / 스키마 일치 |
| **Data Integrity** | Data accuracy / 데이터 정확성 |
| **Headers** | Content-Type, Cache, etc. |

## Automation Tools / 자동화 도구
- Postman/Newman
- REST Assured (Java)
- Supertest (Node.js)
- httpx/requests (Python)
- Bruno, Insomnia
