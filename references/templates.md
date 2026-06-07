# Test Case Common Templates

## Scenario vs Case

| Criteria | Test Scenario | Test Case |
|----------|---------------|-----------|
| **Level** | High-level (What to test) | Low-level (How to test) |
| **Perspective** | Business/User | Executor/Technical |
| **Detail** | Overview | Specific steps |
| **Relation** | 1 Scenario = N Cases | N Cases ⊂ 1 Scenario |
| **Question** | "What situation to test?" | "How to test?" |

### Hierarchy

```
Feature
└── Test Scenario - "What" to test?
    └── Test Case - "How" to test?
        └── Test Step - Execution procedure
```

### Example: Login Feature

**Scenarios (3)**

| ID | Scenario | Type |
|----|----------|------|
| SC-LOGIN-001 | Successful login with valid credentials | Happy Path |
| SC-LOGIN-002 | Login failure with invalid credentials | Exception |
| SC-LOGIN-003 | Login attempt with locked account | Exception |

**Cases for SC-LOGIN-001**

| ID | Case | Input | Expected Result |
|----|------|-------|-----------------|
| TC-LOGIN-001 | Email+Password login | valid@test.com / Pass123! | Redirect to main page |
| TC-LOGIN-002 | Social login (Google) | OAuth auth | Redirect to main page |
| TC-LOGIN-003 | Auto-login enabled | Checkbox selected | Session kept 7 days |

**Cases for SC-LOGIN-002**

| ID | Case | Input | Expected Result |
|----|------|-------|-----------------|
| TC-LOGIN-004 | Non-existent email | wrong@test.com | "Invalid email or password" |
| TC-LOGIN-005 | Wrong password | valid@test.com / wrong | "Invalid email or password" |
| TC-LOGIN-006 | Invalid email format | invalid-email | "Invalid email format" |
| TC-LOGIN-007 | Empty password | valid@test.com / (empty) | "Enter password" |

**Full Structure**

```
Login Feature
├── SC-LOGIN-001: Successful login
│   ├── TC-LOGIN-001: Email+Password
│   ├── TC-LOGIN-002: Social login
│   └── TC-LOGIN-003: Auto-login
├── SC-LOGIN-002: Login failure
│   ├── TC-LOGIN-004: Non-existent email
│   ├── TC-LOGIN-005: Wrong password
│   ├── TC-LOGIN-006: Invalid email format
│   └── TC-LOGIN-007: Empty password
└── SC-LOGIN-003: Account locked
    ├── TC-LOGIN-008: Lock triggered
    └── TC-LOGIN-009: Lock released
```

---

## ID Naming Convention

### Scenario ID
```
SC-[FEATURE]-[NNN]

Example: SC-LOGIN-001, SC-PAYMENT-003, SC-SEARCH-002
```

### Case ID
```
TC-[TYPE]-[NNN] or TC-[FEATURE]-[NNN]

TYPE (by test type):
- UNIT: Unit test
- INT: Integration test
- API: API test
- E2E: E2E test
- SEC: Security test
- PERF: Performance test
- A11Y: Accessibility test

Example: TC-API-001, TC-E2E-015, TC-LOGIN-007
```

## Priority Criteria

| Priority | Criteria | Example |
|----------|----------|---------|
| **Critical** | Core business function, service unavailable if it fails | Login, Payment |
| **High** | Major function, significant UX impact | Search, Order |
| **Medium** | Supporting function, alternative path exists | Filtering, Sorting |
| **Low** | Additional function, minimal impact if unused | UI enhancement, convenience features |

## Detailed Test Case Template

```markdown
## TC-[TYPE]-[NNN]: [Test Title]

### Basic Info
| Item | Content |
|------|---------|
| **ID** | TC-TYPE-NNN |
| **Title** | Clear test purpose |
| **Priority** | Critical / High / Medium / Low |
| **Test Type** | Unit / Integration / API / E2E / Security / Performance / Accessibility |
| **Related Requirement** | REQ-XXX |

### Preconditions
- Condition 1: [State/environment]
- Condition 2: [Required data/settings]

### Test Data
```json
{
  "input": {},
  "expected": {}
}
```

### Test Steps
| # | Step | Input/Action | Expected Result |
|---|------|--------------|-----------------|
| 1 | [Action] | [Input] | [Result] |
| 2 | [Action] | [Input] | [Result] |

### Meta Info
| Item | Content |
|------|---------|
| **Automation** | Possible | Not possible (reason) |
| **Automation Tool** | Jest / Playwright / k6 / etc. |
| **Environment** | Local / Staging / Production |
| **Notes** | Additional info |
```

## Scenario Summary Template

```markdown
# [Feature] Test Scenarios

## Overview
| Item | Content |
|------|---------|
| **Test Target** | [Description] |
| **Test Scope** | [Description] |
| **Test Type** | [Type] |
| **Created** | YYYY-MM-DD |

## Scenario List

| ID | Scenario | Flow Type | Priority | Cases |
|----|----------|-----------|----------|-------|
| SC-001 | Normal login | Happy Path | Critical | 3 |
| SC-002 | Wrong password | Exception | High | 2 |
| SC-003 | Account locked | Exception | High | 2 |

## Coverage Matrix

| Requirement | Scenario | Cases | Status |
|-------------|----------|-------|--------|
| REQ-001 | SC-001, SC-002 | TC-001~005 | Complete |
| REQ-002 | SC-003 | TC-006~007 | In Progress |
```

## Test Result Template

```markdown
# Test Execution Result

## Summary
| Item | Value |
|------|-------|
| **Execution Date** | YYYY-MM-DD |
| **Environment** | Staging |
| **Total Cases** | 50 |
| **Passed** | 45 (90%) |
| **Failed** | 3 (6%) |
| **Skipped** | 2 (4%) |

## Failed Cases
| ID | Title | Failure Reason | Assignee |
|----|-------|----------------|----------|
| TC-API-015 | Large file upload | Timeout | @dev |
```
