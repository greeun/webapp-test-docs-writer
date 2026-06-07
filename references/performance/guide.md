# Performance Test Guide

## Purpose
Verify system performance, stability, and scalability.

## Test Types

| Type | Purpose | Scenario |
|------|---------|----------|
| **Load Test** | Performance under expected load | 100 concurrent users |
| **Stress Test** | Find breaking point | Gradual load increase |
| **Spike Test** | Handle sudden load | Sudden traffic spike |
| **Soak Test** | Long-term stability | 24-hour sustained load |
| **Scalability Test** | Scalability | Performance with resource increase |

## Scenario Derivation Criteria

### 1. Core Transactions
| Function | Target Response Time | Target TPS |
|----------|----------------------|------------|
| Login | < 500ms | 100 |
| Search | < 1s | 200 |
| Create order | < 2s | 50 |
| File upload | < 5s | 20 |

### 2. Load Pattern
```
Ramp-up    → Steady State → Ramp-down
[0→100 VU] → [100 VU hold] → [100→0 VU]
 (2 min)      (10 min)        (1 min)
```

### 3. Metrics
| Metric | Description | Target |
|--------|-------------|--------|
| **Response Time** | Request-response time | p95 < 2s |
| **Throughput** | Requests per second | > 100 TPS |
| **Error Rate** | Error percentage | < 1% |
| **CPU Usage** | CPU utilization | < 80% |
| **Memory Usage** | Memory utilization | < 85% |

## Test Case Example

```markdown
## TC-PERF-001: Login API load test

| Item | Content |
|------|---------|
| **Target** | POST /api/auth/login |
| **Priority** | Critical |

### Load Settings
| Item | Value |
|------|-------|
| Virtual Users | 100 |
| Duration | 10 min |
| Ramp-up | 2 min |
| Target RPS | 50 |

### Test Data
- 100 test accounts
- Random login attempts

### Performance Goals (SLA)
| Metric | Target |
|--------|--------|
| Avg Response Time | < 500ms |
| p95 Response Time | < 1s |
| p99 Response Time | < 2s |
| Error Rate | < 0.5% |
| Throughput | >= 50 RPS |

### Data Collection
- Response time distribution
- Error logs
- Server resource usage
```

## Test Environment

| Environment | Description |
|-------------|-------------|
| **Production-like** | Same specs as production |
| **Isolation** | No other traffic |
| **Monitoring** | APM, server metrics collection |

## Automation Tools
- k6 (Recommended)
- Apache JMeter
- Gatling
- Locust
- Artillery
