# Unit Test Guide

## Purpose
Verify individual functions, methods, and modules in isolation.

## Test Targets
- Pure functions (business logic)
- Utility functions
- Data transformation/parsing
- State management (reducers, stores)
- Custom hooks (React)
- Class methods

## Scenario Derivation Criteria

### 1. Input-based
| Category | Test Case |
|----------|-----------|
| Valid input | Normal operation with valid values |
| Boundary values | Min, max, boundary conditions |
| Invalid input | null, undefined, empty, wrong type |
| Special cases | Empty array, empty object, special chars |

### 2. Branch-based
- Cover all if/else branches
- All switch cases
- Both sides of ternary operators
- Early return conditions

### 3. Exception-based
- All thrown exceptions
- catch paths in try-catch
- Error message accuracy

## Test Case Example

```markdown
## TC-UNIT-001: calculateTotal - Normal calculation

| Item | Content |
|------|---------|
| **Target** | `calculateTotal(items)` |
| **Priority** | High |

### Test Data
| Input | Expected Output |
|-------|-----------------|
| `[{price: 100, qty: 2}]` | `200` |
| `[{price: 100, qty: 2}, {price: 50, qty: 1}]` | `250` |

### Verification
- Return value is number type
- Calculation is accurate
```

## Coverage Goals

| Metric | Target |
|--------|--------|
| Line Coverage | >= 80% |
| Branch Coverage | >= 75% |
| Function Coverage | >= 90% |

## Automation Tools
- JavaScript/TypeScript: Jest, Vitest
- Python: pytest
- Go: testing
- Java: JUnit
