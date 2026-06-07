# Accessibility Test Guide

## Purpose
Ensure WCAG 2.1 compliance and accessibility for all users.

## WCAG Principles (POUR)

| Principle | Description | Example |
|-----------|-------------|---------|
| **Perceivable** | Can be perceived | Alt text, captions |
| **Operable** | Can be operated | Keyboard access, sufficient time |
| **Understandable** | Can be understood | Clear labels, error guidance |
| **Robust** | Robust | Assistive technology compatible |

## Scenario Derivation Criteria

### 1. Visual Accessibility
| Item | Test Content | WCAG |
|------|--------------|------|
| Alt text | Images have alt attribute | 1.1.1 |
| Contrast | Text 4.5:1 or higher | 1.4.3 |
| Text size | Usable at 200% zoom | 1.4.4 |
| Color dependence | No info conveyed by color alone | 1.4.1 |

### 2. Keyboard Accessibility
| Item | Test Content | WCAG |
|------|--------------|------|
| Keyboard navigation | Tab reaches all elements | 2.1.1 |
| Focus indicator | Visual indication of current position | 2.4.7 |
| Keyboard trap | Not trapped in any element | 2.1.2 |
| Shortcuts | No conflicting shortcuts | 2.1.4 |

### 3. Screen Reader Compatibility
| Item | Test Content | WCAG |
|------|--------------|------|
| Semantic markup | Correct HTML elements used | 1.3.1 |
| Landmarks | main, nav, header, etc. | 1.3.1 |
| Form labels | input and label connected | 1.3.1 |
| Dynamic content | aria-live announcements | 4.1.3 |

### 4. Cognitive Accessibility
| Item | Test Content | WCAG |
|------|--------------|------|
| Error messages | Clear error description | 3.3.1 |
| Input hints | Expected format guidance | 3.3.2 |
| Consistent navigation | Same menu structure | 3.2.3 |
| Sufficient time | Timeout extension option | 2.2.1 |

## Test Case Example

```markdown
## TC-A11Y-001: Login form keyboard accessibility

| Item | Content |
|------|---------|
| **WCAG** | 2.1.1 (Keyboard) |
| **Priority** | High |

### Preconditions
- No mouse used
- Screen reader enabled (VoiceOver/NVDA)

### Test Steps
| # | Step | Expected Result |
|---|------|-----------------|
| 1 | Tab to email field | Focus visible, label read |
| 2 | Enter email | Input possible |
| 3 | Tab to password | Focus visible, label read |
| 4 | Submit with Enter | Login executes |
| 5 | On error | Error message auto-read |

### Verification
- [ ] All elements accessible via Tab
- [ ] Focus visually indicated
- [ ] Screen reader labels accurate
- [ ] Form submittable via keyboard
```

## Test Tools

| Tool | Purpose |
|------|---------|
| **axe DevTools** | Automated testing |
| **WAVE** | Web accessibility evaluation |
| **Lighthouse** | Accessibility score |
| **VoiceOver** | macOS screen reader |
| **NVDA** | Windows screen reader |
| **Color Contrast Analyzer** | Contrast check |

## Compliance Levels

| Level | Description |
|-------|-------------|
| **A** | Minimum requirements |
| **AA** | Recommended (legal standard) |
| **AAA** | Highest level |

Target: **WCAG 2.1 Level AA** compliance
