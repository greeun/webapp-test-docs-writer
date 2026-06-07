# Integration Test Guide

## Purpose
Verify that multiple components/modules work correctly together.

## Test Targets
- Service layer ↔ Database
- Component ↔ API client
- State management ↔ UI component
- External service integration
- Event publish/subscribe

## Scenario Derivation Criteria

### 1. Data Flow
| Category | Verification Point |
|----------|--------------------|
| Input → Process → Save | Data integrity |
| Query → Transform → Output | Data consistency |
| Event publish → Subscribe → Process | Event delivery |

### 2. State Changes
- Initial state → Action → Changed state
- Chained state changes (A → B → C)
- State recovery on rollback/failure

### 3. Transactions
- Commit on success
- Rollback on failure
- Partial failure handling

## Test Case Example

```markdown
## TC-INT-001: User creation and retrieval

| Item | Content |
|------|---------|
| **Scope** | UserService ↔ UserRepository ↔ Database |
| **Priority** | Critical |

### Preconditions
- Test DB connected
- users table is empty

### Test Steps
| # | Step | Expected Result |
|---|------|-----------------|
| 1 | Call `userService.create({name: "Kim"})` | Returns created user object |
| 2 | Call `userService.findById(id)` | Returns same user |
| 3 | Direct DB query | Record exists |

### Cleanup
- Delete created test data
```

## Test Environment

| Environment | Description |
|-------------|-------------|
| **Test DB** | Use a dedicated test DB |
| **Mock Server** | Mock external APIs |
| **Isolation** | Data isolation between tests |

## Automation Tools
- Jest + Supertest (Node.js)
- pytest + TestClient (Python/FastAPI)
- Spring Boot Test (Java)
- Testcontainers (Docker-based)
