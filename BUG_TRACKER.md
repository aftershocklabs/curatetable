# CurateTable - Bug Tracker

> **Last Updated:** February 14, 2026
> **Status Key:** `OPEN` | `IN_PROGRESS` | `RESOLVED` | `CLOSED` | `WONT_FIX`
> **Severity:** `P0` Critical | `P1` High | `P2` Medium | `P3` Low

---

## How to Report a Bug

When filing a bug, include the following:

```markdown
### BUG-XXX: [Short Description]

- **Severity:** P0/P1/P2/P3
- **Status:** OPEN
- **Reported By:** [Name]
- **Date Reported:** YYYY-MM-DD
- **Assigned To:** [Name]
- **Environment:** Development / Staging / Production
- **Browser/Device:** [e.g., Chrome 120 / macOS]

**Steps to Reproduce:**
1. Step one
2. Step two
3. Step three

**Expected Behavior:**
What should happen.

**Actual Behavior:**
What actually happens.

**Screenshots/Logs:**
[Attach if applicable]

**Root Cause (if known):**
[Analysis]

**Fix:**
[Description of fix or PR link]

**Date Resolved:** YYYY-MM-DD
```

---

## Bug Categories

| Category | Description |
|----------|------------|
| `UI` | Visual/layout issues, styling bugs, responsive design problems |
| `AI` | AI response quality, conversation flow, data extraction errors |
| `API` | Backend endpoint failures, incorrect responses, timeouts |
| `DB` | Database errors, data integrity issues, migration problems |
| `PDF` | PDF generation failures, formatting issues, missing data |
| `EMAIL` | Email delivery failures, template rendering issues |
| `PERF` | Performance issues, slow load times, memory leaks |
| `SEC` | Security vulnerabilities, data exposure, injection risks |
| `A11Y` | Accessibility issues, WCAG violations |
| `INTEG` | Third-party integration failures (Google Maps, SAP, etc.) |

---

## Active Bugs

> No bugs reported yet. Project is in pre-development phase.

---

## Bug Log

### Phase 1 (MVP)

| ID | Title | Category | Severity | Status | Assigned | Date |
|----|-------|----------|----------|--------|----------|------|
| — | — | — | — | — | — | — |

### Phase 2 (Scale)

| ID | Title | Category | Severity | Status | Assigned | Date |
|----|-------|----------|----------|--------|----------|------|
| — | — | — | — | — | — | — |

### Phase 3 (Marketplace)

| ID | Title | Category | Severity | Status | Assigned | Date |
|----|-------|----------|----------|--------|----------|------|
| — | — | — | — | — | — | — |

---

## Bug Metrics

| Metric | Value |
|--------|-------|
| Total Bugs Reported | 0 |
| Open | 0 |
| In Progress | 0 |
| Resolved | 0 |
| Closed | 0 |
| Won't Fix | 0 |
| Avg Resolution Time | — |

---

## Severity Definitions

### P0 — Critical
- Application crash or data loss
- Security vulnerability
- Core feature completely broken
- No workaround available
- **SLA:** Fix within 4 hours

### P1 — High
- Core feature partially broken
- Significant degradation of user experience
- Workaround exists but is painful
- **SLA:** Fix within 24 hours

### P2 — Medium
- Non-core feature broken
- Minor visual/layout issues
- Workaround is reasonable
- **SLA:** Fix within 1 week

### P3 — Low
- Cosmetic issues
- Edge case bugs
- Minor inconvenience
- **SLA:** Fix in next sprint

---

## Bug Triage Process

1. **Report:** Bug filed with all required fields
2. **Triage:** Assign severity and category (daily review)
3. **Assign:** Assign to team member based on category
4. **Investigate:** Reproduce, identify root cause
5. **Fix:** Implement fix with tests (TDD — write failing test first)
6. **Review:** Code review + QA verification
7. **Close:** Update status, document resolution

### Triage Meeting
- **Frequency:** Daily during active development, weekly during maintenance
- **Attendees:** Funky (Engineering), Peepu (Product)
- **Agenda:** Review new bugs, update priorities, unblock in-progress items

---

## Known Issues / Tech Debt

> Track technical debt and known limitations that aren't bugs per se.

| ID | Description | Category | Impact | Priority |
|----|-------------|----------|--------|----------|
| TD-001 | TBD | — | — | — |

---

## Regression Test Checklist

Before every release, verify these critical paths:

- [ ] **Chat flow:** User can start conversation and receive AI responses
- [ ] **Data extraction:** AI correctly extracts restaurant profile from conversation
- [ ] **Location:** Address autocomplete works and returns demographics
- [ ] **Recommendations:** System returns scored product recommendations
- [ ] **PDF generation:** Catalog PDF generates with correct products and branding
- [ ] **PDF download:** Generated PDF can be downloaded successfully
- [ ] **Email:** Catalog can be sent via email with PDF attachment
- [ ] **Responsive:** All pages render correctly on mobile (375px+)
- [ ] **Accessibility:** No critical aXe violations
- [ ] **Performance:** Lighthouse score 90+ on all categories
