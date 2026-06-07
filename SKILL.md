---
name: webapp-test-docs-writer
version: 1.0.0
description: |
  Write test scenarios and test cases for web service verification. Generate test documents based on functional specs, API specs, and code analysis for Unit/Integration/API/E2E/Security/Performance/Accessibility testing.
  Triggers: "test case", "test scenario", "write tests", "QA documentation", "테스트 케이스 작성", "테스트 시나리오", "QA 문서"
---

# Webapp Test Docs Writer

Write test scenarios and test cases for web service verification.

## Language

Detect the user's language and respond in that language.

- English request → English output
- Korean request → Korean output

## Workflow

```
1. Analyze Input → 2. Select Test Type → 3. Derive Scenarios → 4. Write Cases → 5. Review
```

### Step 0: Dedup Check (MANDATORY)

Before writing any test scenario or case, perform these checks:

1. **Read dedup policy**: If `docs/testing/TEST_DEDUP_POLICY.md` exists, read and enforce it
2. **Search existing tests**: `grep -r "target_endpoint_or_function" tests/ -l`
3. **Layer ownership**: Each item belongs to ONE layer only
   - Pure function → unit | API endpoint → api | Browser flow → e2e | OWASP → security
   - Auth 401/403 → per-feature api file only (NOT bulk security files)
4. **If an existing file is found**: Add the TC to that file (do NOT create a new file)
5. **Prohibited patterns**:
   - Placeholder TC with no real assertions
   - Duplicate TC across layers
   - TC for unimplemented features
   - Aggregation files bundling separate endpoints

### Step 1: Analyze Input

| Source | Check |
|--------|-------|
| **Functional Spec** | Requirements, user stories, acceptance criteria |
| **API Spec** | Endpoints, request/response schema, status codes |
| **Code** | Business logic, branching, exception handling |

### Step 2: Select Test Type

| Type | Purpose | Guide |
|------|---------|-------|
| **Unit** | Verify individual functions/modules | [references/unit/](references/unit/) |
| **Integration** | Verify component interactions | [references/integration/](references/integration/) |
| **API** | Verify REST/GraphQL endpoints | [references/api/](references/api/) |
| **E2E** | Verify complete user flows | [references/e2e/](references/e2e/) |
| **Security** | Verify security vulnerabilities | [references/security/](references/security/) |
| **Performance** | Verify performance/load | [references/performance/](references/performance/) |
| **Accessibility** | Verify WCAG compliance | [references/accessibility/](references/accessibility/) |

### Step 3: Derive Scenarios

For each feature, derive scenarios from these perspectives:

1. **Happy Path** - Expected behavior
2. **Alternative** - Success via a different path
3. **Exception** - Error/failure cases
4. **Boundary** - Min/max/boundary conditions

### Step 4: Write Cases

Use templates from [references/templates.md](references/templates.md).

**Required fields:**

| Field | Description |
|-------|-------------|
| ID | Unique identifier (e.g., TC-API-001) |
| Title | Clear test purpose |
| Preconditions | Required state before test |
| Test Steps | Sequential execution steps |
| Expected Results | Expected outcome per step |
| Priority | Critical / High / Medium / Low |
| Test Data | Input data and examples |
| Automation | Automation feasibility |

### Step 5: Review Checklist

- [ ] 100% requirements coverage
- [ ] Both positive/negative cases
- [ ] Boundary tests included
- [ ] Test data is clear
- [ ] Steps are reproducible
- [ ] Expected results are verifiable

## Output Format

### Scenario Document

```markdown
# [Feature] Test Scenarios

## Overview
| Item | Content |
|------|---------|
| Target | [Test target] |
| Scope | [Test scope] |
| Test Type | [Unit/Integration/API/E2E/Security/Performance/Accessibility] |

## Scenario List

| ID | Scenario | Type | Priority |
|----|----------|------|----------|
| SC-001 | [Description] | Happy Path | High |
```

### Test Case Document

```markdown
## TC-[TYPE]-[NNN]: [Test Title]

| Item | Content |
|------|---------|
| **Priority** | High |
| **Preconditions** | - Condition 1<br>- Condition 2 |
| **Test Data** | `{"key": "value"}` |

### Test Steps

| # | Step | Expected Result |
|---|------|-----------------|
| 1 | [Action] | [Result] |
| 2 | [Action] | [Result] |

### Meta Info
- Automation: Possible | Not possible
- Related Requirement: REQ-001
- Notes: [Additional info]
```

## Quick Start

When a user requests test writing:

1. Identify the test target (feature/API/page)
2. Refer to the relevant test type guide
3. Derive scenarios then write cases
4. Output in Markdown table format
