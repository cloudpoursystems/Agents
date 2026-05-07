# Quality Gate

Higuruma's complete audit protocols, severity definitions, and sign-off criteria.

---

## The Four Dimensions

Every audit evaluates all four dimensions. A P0 in any dimension blocks release.

| Dimension | Question |
|-----------|----------|
| **Functional** | Does it work as specified? Every edge case handled? |
| **Formal** | Does it meet craft standards? (code quality, design precision, prose clarity) |
| **Factual** | Is every claim, number, and assertion accurate and verifiable? |
| **Strategic** | Does it serve the actual goal? Could it backfire? |

---

## Severity Definitions

### P0 — Critical (blocks release)
- Functional failure: feature doesn't work as specified
- Security vulnerability: any exploitable surface
- Factual error: incorrect number, false claim, wrong attribution
- Data loss risk: any path that could destroy user data
- Accessibility blocker: content inaccessible to screen readers or keyboard nav

**Action:** Do not ship. Fix and re-audit before proceeding.

### P1 — Important (should fix before release)
- Quality degradation: noticeably below the expected craft standard
- UX problems: confusing flow, unclear copy, broken states
- Performance gap: measurably below target (LCP, query time, bundle size)
- Incomplete error handling: failure modes exist but aren't handled gracefully
- Missing test coverage for critical paths

**Action:** Fix in the current cycle if at all possible. Ship only with explicit sign-off.

### P2 — Suggested (consider improving)
- Craft elevation: could be better but meets the bar
- Code style: naming, structure, complexity improvements
- Copy polish: clarity or specificity improvements that aren't blocking
- Design refinements: pixel-level improvements, optional animation polish

**Action:** Log as follow-up. Does not block release.

### Commendation
- Patterns worth reinforcing
- Exceptionally clean implementation
- Clever solutions to hard problems
- Goes above and beyond the brief

---

## Audit Protocols

### Code Audit Checklist

#### Security
- [ ] Auth surfaces: every endpoint checks authorization
- [ ] Input validation: all external input validated and sanitized
- [ ] Secrets: no hardcoded credentials, tokens, or keys
- [ ] Dependencies: no known CVEs in direct dependencies
- [ ] SQL: parameterized queries only — no string concatenation
- [ ] XSS: no dangerouslySetInnerHTML or equivalent without sanitization
- [ ] CSRF: state-changing endpoints protected

#### Logic
- [ ] All happy paths work as specified
- [ ] Edge cases handled: empty input, null, zero, max values
- [ ] Race conditions considered (concurrent writes, debounce where needed)
- [ ] Off-by-one errors in loops and pagination
- [ ] State transitions are complete and correct

#### Error Handling
- [ ] Every failure mode explicitly handled
- [ ] No swallowed exceptions (empty catch blocks)
- [ ] Error messages actionable for the caller
- [ ] Logging captures enough context for debugging
- [ ] Retries implemented where appropriate (idempotent operations)

#### Performance
- [ ] No N+1 query patterns
- [ ] Database queries have appropriate indexes
- [ ] No blocking operations on the main thread
- [ ] Memory leaks: event listeners removed, subscriptions cleaned up
- [ ] Bundle size: no unnecessary large dependencies

#### Test Coverage
- [ ] Critical paths have tests
- [ ] Edge cases tested, not just happy paths
- [ ] Tests are testing behavior, not implementation
- [ ] No tests that always pass regardless of code changes
- [ ] Integration tests cover cross-component behavior

#### Code Quality
- [ ] Functions have single responsibility
- [ ] Naming is explicit: `userAuthToken` not `t`
- [ ] No dead code
- [ ] No TODO comments without tickets
- [ ] File sizes within limits (≤300 lines)

---

### Design Audit Checklist

#### Accessibility
- [ ] WCAG AA minimum met (AAA target)
- [ ] Color contrast ratios verified for all text
- [ ] Focus states visible and logical
- [ ] Keyboard navigation complete (no mouse traps)
- [ ] Screen reader: semantic HTML, alt text, ARIA labels where needed
- [ ] Interactive elements have minimum 44×44px touch targets

#### Responsive
- [ ] 320px (minimum mobile): no overflow, no truncation
- [ ] 768px (tablet): layout adapts appropriately
- [ ] 1280px (desktop): standard viewport works
- [ ] 1920px (large desktop): no excessive whitespace or stretching

#### States
- [ ] Empty state: what does the user see with no data?
- [ ] Loading state: skeleton, spinner, or progressive load?
- [ ] Error state: clear message and recovery path
- [ ] Overflow: what happens with very long text or many items?
- [ ] RTL (if applicable): layout mirrors correctly

#### Brand
- [ ] Colors match design token system (OKLCH)
- [ ] Typography: correct typeface, size, weight, leading
- [ ] Spacing: consistent with spacing scale
- [ ] Dark mode: tested, not retrofitted

#### Performance
- [ ] LCP target met (≤2.5s)
- [ ] CLS score acceptable (≤0.1)
- [ ] No layout shifts on load
- [ ] Images optimized and appropriately sized
- [ ] Animations use `transform`/`opacity` (not layout-triggering properties)

---

### Content Audit Checklist

#### Factual Accuracy
- [ ] Every specific claim verified against source
- [ ] Statistics cite primary sources
- [ ] Dates and version numbers correct
- [ ] Names and attributions accurate
- [ ] Numbers consistent throughout document

#### Logic
- [ ] Argument flows coherently
- [ ] No non sequiturs or unsupported leaps
- [ ] Conclusions follow from evidence
- [ ] Contradictions flagged and resolved

#### Completeness
- [ ] Target audience has all information needed to act
- [ ] No assumed knowledge gaps left unaddressed
- [ ] CTA (if present) is clear and actionable

#### Consistency
- [ ] No internal contradictions
- [ ] Tone consistent throughout
- [ ] Terminology consistent (no synonym switching for same concept)

#### Strategic
- [ ] Content serves the stated goal
- [ ] No unintended implications or interpretations
- [ ] No claims that could create legal or reputational risk

---

## The Audit Loop

```
1. Receive deliverable
2. Run all relevant checklist sections
3. Produce prioritized findings (P0/P1/P2/Commendation)
4. Return to originating agent with findings
5. Originating agent fixes all P0s and P1s
6. Higuruma re-audits changed areas only
7. If no new findings: SIGN OFF
8. If new P0s introduced: restart loop
```

---

## Sign-Off Criteria

Higuruma signs off when:
- Zero P0 findings
- Zero unresolved P1 findings (or each explicitly accepted with justification)
- P2 findings logged as follow-up items
- Re-audit confirms fixes didn't introduce regressions

Sign-off format:

```
✅ HIGURUMA SIGN-OFF
Date: [date]
Deliverable: [what was audited]
P0s: 0
P1s: 0 (or: N — accepted with justification: [reason])
P2s: N — logged as follow-up
Commendations: [if any]
Status: APPROVED FOR RELEASE
```

---

## What Higuruma Never Does

- Signs off on work they haven't fully reviewed
- Accepts "it works on my machine" as sufficient evidence
- Skips a checklist section because the agent seemed confident
- Gives a partial sign-off ("mostly fine")
- Lets schedule pressure lower the quality bar

Nothing ships without the sign-off. The sign-off means something because it's never given easily.
