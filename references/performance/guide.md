# Performance Test Guide / 성능 테스트 가이드

## Purpose / 목적
Verify system performance, stability, and scalability.
시스템의 성능, 안정성, 확장성 검증.

## Test Types / 테스트 유형

| Type / 유형 | Purpose / 목적 | Scenario / 시나리오 |
|-------------|----------------|---------------------|
| **Load Test** | Performance under expected load / 예상 부하에서 성능 | 100 concurrent users / 100명 동시 접속 |
| **Stress Test** | Find breaking point / 한계점 파악 | Gradual load increase / 점진적 부하 증가 |
| **Spike Test** | Handle sudden load / 급격한 부하 대응 | Sudden traffic spike / 갑작스러운 트래픽 |
| **Soak Test** | Long-term stability / 장시간 안정성 | 24-hour sustained load / 24시간 지속 부하 |
| **Scalability Test** | Scalability / 확장성 | Performance with resource increase / 리소스 증가 시 성능 |

## Scenario Derivation Criteria / 시나리오 도출 기준

### 1. Core Transactions / 핵심 트랜잭션
| Function / 기능 | Target Response Time / 목표 응답시간 | Target TPS / 목표 TPS |
|-----------------|-------------------------------------|----------------------|
| Login / 로그인 | < 500ms | 100 |
| Search / 검색 | < 1s | 200 |
| Create order / 주문 생성 | < 2s | 50 |
| File upload / 파일 업로드 | < 5s | 20 |

### 2. Load Pattern / 부하 패턴
```
Ramp-up    → Steady State → Ramp-down
[0→100 VU] → [100 VU hold] → [100→0 VU]
 (2 min)      (10 min)        (1 min)
```

### 3. Metrics / 측정 지표

| Metric / 지표 | Description / 설명 | Target / 목표 |
|---------------|-------------------|---------------|
| **Response Time** | Request-response time / 요청-응답 시간 | p95 < 2s |
| **Throughput** | Requests per second / 초당 처리량 | > 100 TPS |
| **Error Rate** | Error percentage / 오류 비율 | < 1% |
| **CPU Usage** | CPU utilization / CPU 사용률 | < 80% |
| **Memory Usage** | Memory utilization / 메모리 사용률 | < 85% |

## Test Case Example / 테스트 케이스 예시

```markdown
## TC-PERF-001: Login API load test / 로그인 API 부하 테스트

| Item / 항목 | Content / 내용 |
|-------------|----------------|
| **Target / 대상** | POST /api/auth/login |
| **Priority / 우선순위** | Critical |

### Load Settings / 부하 설정
| Item / 항목 | Value / 값 |
|-------------|------------|
| Virtual Users | 100 |
| Duration / 지속시간 | 10 min / 10분 |
| Ramp-up | 2 min / 2분 |
| Target RPS | 50 |

### Test Data / 테스트 데이터
- 100 test accounts / 100명의 테스트 계정
- Random login attempts / 랜덤 로그인 시도

### Performance Goals (SLA) / 성능 목표
| Metric / 지표 | Target / 목표 |
|---------------|---------------|
| Avg Response Time | < 500ms |
| p95 Response Time | < 1s |
| p99 Response Time | < 2s |
| Error Rate | < 0.5% |
| Throughput | >= 50 RPS |

### Data Collection / 결과 수집
- Response time distribution / 응답 시간 분포
- Error logs / 에러 로그
- Server resource usage / 서버 리소스 사용량
```

## Test Environment / 테스트 환경

| Environment / 환경 | Description / 설명 |
|--------------------|-------------------|
| **Production-like** | Same specs as production / 실제와 동일한 스펙 |
| **Isolation / 격리** | No other traffic / 다른 트래픽 없음 |
| **Monitoring / 모니터링** | APM, server metrics collection / APM, 서버 메트릭 수집 |

## Automation Tools / 자동화 도구
- k6 (Recommended / 권장)
- Apache JMeter
- Gatling
- Locust
- Artillery
