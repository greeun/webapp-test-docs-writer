# E2E Test Guide

## Purpose
Verify complete system flows from the real user's perspective.

## Test Targets
- Core user scenarios
- Page navigation
- Form input and submission
- Auth flow (login/logout)
- Core business flows (payment, order)

## Scenario Derivation Criteria

### 1. User Journey
| Category | Example |
|----------|---------|
| New user | Sign up → Email verification → Profile setup |
| Buyer | Search → Select product → Cart → Checkout |
| Admin | Login → Dashboard → View/Edit data |

### 2. Core Function Flows
- Login → Main → Use feature → Logout
- Error occurs → Error page → Recovery
- Session expired → Re-login → Restore state

### 3. Cross Browser/Device
- Chrome, Firefox, Safari
- Desktop, Tablet, Mobile
- Responsive layout

## Test Case Example

```markdown
## TC-E2E-001: Complete sign-up flow

| Item | Content |
|------|---------|
| **Scenario** | New user completes sign-up |
| **Priority** | Critical |
| **Expected Duration** | 2 min |

### Preconditions
- Test email available
- Browser: Chrome latest

### Test Steps
| # | Page | Action | Expected Result |
|---|------|--------|-----------------|
| 1 | Home | Click "Sign Up" | Sign-up form displayed |
| 2 | Sign Up | Enter email | Validation passes |
| 3 | Sign Up | Enter password | Strength indicator |
| 4 | Sign Up | Click "Sign Up" button | Verification email notice |
| 5 | Email | Click verification link | Completion page |
| 6 | Complete | Auto-login | Main page, username displayed |

### Verification
- [ ] URL changes at each step
- [ ] No error messages
- [ ] User created in DB
```

## Test Design Principles

| Principle | Description |
|-----------|-------------|
| **Independence** | Each test can run independently |
| **Repeatability** | Same results can be reproduced |
| **Stability** | Minimize flaky tests |
| **Readability** | Clear intent in steps |

## Automation Tools
- Playwright (Recommended)
- Cypress
- Selenium WebDriver
- Puppeteer
