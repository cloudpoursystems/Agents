# Validation Checklist

Per-agent critical and non-critical checks for validating agent definitions, behavior, and output quality.

Use this checklist when: modifying an agent definition, adding a new agent, debugging unexpected agent behavior, or running a periodic quality audit of the agent system.

---

## How to Run Validation

For each check, run a test prompt and evaluate the output against the criteria.

**Pass:** Output meets the criterion  
**Fail:** Output does not meet the criterion — investigate agent definition  
**N/A:** Check does not apply to the current context

---

## System-Level Checks (All Agents)

These apply to every agent in the system.

### Critical

- [ ] Agent responds to `@agentname` prefix correctly
- [ ] Agent frontmatter `name:` field matches the invocation name
- [ ] Agent frontmatter `model:` is set to `claude-opus-4-7`
- [ ] Agent invokes the `Skill` tool before starting substantive work
- [ ] Agent refuses to act outside its defined domain without escalation
- [ ] Agent produces structured output, not stream-of-consciousness prose
- [ ] Agent does not hallucinate skills that aren't in its registry

### Non-Critical

- [ ] Agent uses domain-specific terminology correctly
- [ ] Agent references the correct source of truth (web for external, DB for internal)
- [ ] Agent output format is consistent across runs
- [ ] Agent's system prompt persona is reflected in tone and approach

---

## toji — Software Engineer

### Critical

- [ ] **TDD:** Writes a failing test before implementation on every feature request
- [ ] **No security holes:** Code produced does not contain SQL injection, XSS, hardcoded secrets, or auth bypasses
- [ ] **Error handling:** Every failure path is explicitly handled — no empty catch blocks
- [ ] **No magic numbers:** All constants are named
- [ ] **File size:** Generated files stay under 300 lines unless justified
- [ ] **Function size:** Functions stay under 20 lines unless justified
- [ ] **Test first:** When asked to debug, writes a reproducing test before fixing

### Non-Critical

- [ ] Follows single responsibility principle for functions and modules
- [ ] Uses explicit naming (`userAuthToken`, not `t`)
- [ ] Prefers stdlib over adding dependencies
- [ ] Leaves codebase in better state than found
- [ ] Comments explain WHY, not WHAT

### Test Prompts

```
Validation prompt 1 (TDD check):
@toji Add a function that validates an email address.

Expected: toji writes a failing test first, then the implementation.
Pass if: Test comes before implementation in the output.
Fail if: Implementation appears without a test, or test comes after.
```

```
Validation prompt 2 (security check):
@toji Build a search endpoint that takes a user query and searches the database.

Expected: Parameterized query, not string concatenation.
Pass if: Uses prepared statements or parameterized queries.
Fail if: Builds SQL by concatenating user input.
```

---

## hisoka — Designer

### Critical

- [ ] **OKLCH only:** Uses `oklch()` color functions — never raw hex or HSL
- [ ] **CSS tokens:** Colors, spacing, and typography use CSS custom properties
- [ ] **WCAG:** Generated HTML/CSS meets WCAG AA at minimum (verify with contrast checker)
- [ ] **Mobile-first:** CSS is written mobile-first with `min-width` media queries
- [ ] **Dark mode:** Dark mode is designed simultaneously, not retrofitted
- [ ] **All states:** Every interactive element has hover, focus, active, disabled states

### Non-Critical

- [ ] No Lorem Ipsum — uses realistic placeholder content
- [ ] No gradients without visual purpose
- [ ] Animations are ≤300ms unless intentional
- [ ] Typography has proper optical sizing, kerning, leading
- [ ] Avoids AI aesthetic clichés

### Test Prompts

```
Validation prompt 1 (OKLCH check):
@hisoka Design a button component with primary and secondary variants.

Expected: Colors expressed as oklch() values.
Pass if: oklch() used exclusively for all color values.
Fail if: hex (#fff), rgb(), or hsl() appear in color declarations.
```

```
Validation prompt 2 (states check):
@hisoka Design an input field component.

Expected: Styles for default, focus, error, disabled states.
Pass if: All 4 states have distinct visual treatment.
Fail if: Only default state is designed.
```

---

## gon — Researcher

### Critical

- [ ] **Multi-source:** Every key claim is supported by at least 3 independent sources
- [ ] **Confidence ratings:** Output includes High/Medium/Low confidence for each major finding
- [ ] **Contradictions surfaced:** If sources disagree, both positions are reported
- [ ] **Recency flagged:** Sources older than 18 months in fast-moving domains are flagged
- [ ] **No confirmation bias:** Output challenges the user's assumptions, not just confirms them

### Non-Critical

- [ ] Identifies bias in sources (funder, publisher, methodology)
- [ ] Includes "Gaps & Limitations" section
- [ ] Suggests next research steps
- [ ] Grades source quality (primary / meta-analysis / expert / secondary)

### Test Prompts

```
Validation prompt 1 (multi-source check):
@gon What is the average restaurant profit margin?

Expected: Multiple sources cited, confidence rating included.
Pass if: 3+ sources, confidence rating present, contradictory data surfaced if exists.
Fail if: Single source, no confidence rating, no contradictions mentioned.
```

```
Validation prompt 2 (anti-confirmation-bias check):
@gon Research whether content marketing is effective for B2B SaaS.

Expected: Both supporting evidence AND counterevidence presented.
Pass if: Limitations and cases where it doesn't work are included.
Fail if: Only positive evidence presented.
```

---

## yuji — Writer

### Critical

- [ ] **No banned words:** "innovative," "cutting-edge," "seamless," "leverage," "synergy," "solutions," "empower," "game-changing," "revolutionize" never appear
- [ ] **Specificity:** Uses numbers and names instead of vague adjectives ("saves 3 hours/week" not "saves time")
- [ ] **One job per piece:** Each content piece has a single, clear CTA
- [ ] **Customer-first:** Does not open with "We/Our company"
- [ ] **Lede first:** Most important point appears in the first sentence/paragraph

### Non-Critical

- [ ] Copy reads cleanly aloud (no tongue-twisters or awkward constructions)
- [ ] Word count is appropriate for channel (email ≠ blog post)
- [ ] Brand voice maintained throughout
- [ ] Internal consistency (no synonym-switching for same concept)

### Test Prompts

```
Validation prompt 1 (banned words check):
@yuji Write a tagline for a project management software product.

Expected: No banned words.
Pass if: Output contains none of the banned words.
Fail if: Any of the banned words appear.
```

```
Validation prompt 2 (specificity check):
@yuji Write a value proposition for our analytics dashboard product.

Expected: Specific, quantified benefits.
Pass if: Concrete numbers, timeframes, or comparisons used.
Fail if: Vague adjectives like "powerful," "easy," "efficient" without specifics.
```

---

## higuruma — Quality Auditor

### Critical

- [ ] **P0/P1/P2 format:** Audit output uses the severity framework, not free-form commentary
- [ ] **Blocks on P0:** Explicitly states the deliverable cannot ship with P0 findings
- [ ] **Re-audit:** After fixes are applied, audits changed areas again before signing off
- [ ] **Sign-off is explicit:** Sign-off format is clear and unambiguous
- [ ] **No social pressure:** Does not lower the bar because the team "worked hard" or deadline is close

### Non-Critical

- [ ] Commendations included when work is genuinely excellent
- [ ] Specific file:line references for code findings
- [ ] Specific claim references for content findings
- [ ] Distinguishes between "must fix" and "consider improving"

### Test Prompts

```
Validation prompt 1 (P0 blocking check):
@higuruma Review this code: [code with an obvious SQL injection vulnerability]

Expected: Finding classified as P0 with explicit block on shipping.
Pass if: SQL injection is caught, rated P0, shipping explicitly blocked.
Fail if: Issue is missed, rated lower than P0, or ship is not blocked.
```

```
Validation prompt 2 (format check):
@higuruma Audit this short piece of copy: [paste any content]

Expected: Findings in P0/P1/P2 format.
Pass if: Each finding has a severity prefix.
Fail if: Findings are in free-form prose without severity.
```

---

## pain — DevOps Engineer

### Critical

- [ ] **No secrets in IaC:** Generated Terraform/config never hardcodes credentials or API keys
- [ ] **Rollback included:** Every infrastructure change includes a rollback procedure
- [ ] **Least privilege:** IAM policies are scoped to minimum required permissions
- [ ] **State management:** Terraform state uses remote backend (S3/GCS), not local
- [ ] **Staging first:** Deployment procedures include staging validation before production

### Non-Critical

- [ ] Cost impact estimated for infrastructure changes
- [ ] Monitoring checks specified for post-deployment
- [ ] Incident runbooks are blameless and action-oriented
- [ ] Immutable infrastructure preferred over mutable

### Test Prompts

```
Validation prompt 1 (no secrets check):
@pain Write Terraform for an RDS database with a username and password.

Expected: Credentials referenced from AWS Secrets Manager or variable, not hardcoded.
Pass if: No literal credentials in the Terraform code.
Fail if: username = "admin", password = "password123" or similar appears.
```

```
Validation prompt 2 (rollback check):
@pain Write a deployment procedure for a new API version.

Expected: Rollback procedure explicitly included.
Pass if: Rollback steps are present.
Fail if: No rollback path documented.
```

---

## sukuna — Data Analyst

### Critical

- [ ] **No SELECT *:** SQL output never uses SELECT *, always names columns explicitly
- [ ] **Filters early:** SQL WHERE clauses applied before JOIN where possible
- [ ] **CTEs over nesting:** Complex queries use CTEs, not nested subqueries
- [ ] **Actionable conclusion:** Analysis always ends with "so what? now what?"
- [ ] **Correlation caveat:** Never presents correlation as causation without noting the distinction
- [ ] **Sample size check:** A/B test analyses include sample size adequacy check

### Non-Critical

- [ ] Row counts and sanity checks included in exploratory queries
- [ ] SQL includes comments explaining assumptions
- [ ] Dashboard specs specify what to highlight, not just what to show
- [ ] Segmentation before aggregation (never reports only averages)

### Test Prompts

```
Validation prompt 1 (SELECT * check):
@sukuna Write a query to get all user data for active users.

Expected: Named columns, not SELECT *.
Pass if: Specific column names are listed.
Fail if: SELECT * appears.
```

```
Validation prompt 2 (actionable conclusion check):
@sukuna Analyze this A/B test: [provide sample data with clear winner]

Expected: Recommendation to ship or kill, not just statistics.
Pass if: Clear recommendation + rationale included.
Fail if: Output ends with statistics without a recommendation.
```

---

## grimmjow — Growth Strategist

### Critical

- [ ] **Retention before acquisition:** If retention metrics are poor, flags this before recommending acquisition spend
- [ ] **Unit economics check:** Paid channel recommendations include CAC/LTV sanity check
- [ ] **Stage-appropriate channel:** Does not recommend paid for pre-PMF stage without caveats
- [ ] **CRO hierarchy:** CRO recommendations follow the correct order (UX fix → copy → friction → persuasion → personalization)

### Non-Critical

- [ ] Growth model referenced (Acquisition → Activation → Retention → Revenue → Referral)
- [ ] Distinguishes between leading indicators and lagging metrics
- [ ] Referral program mechanics include viral coefficient consideration
- [ ] Hospitality/beverage context applied when relevant

### Test Prompts

```
Validation prompt 1 (retention-first check):
@grimmjow Our MRR churn is 8% monthly and we want to run paid ads to grow.

Expected: Flag the churn problem before recommending paid.
Pass if: Agent addresses the retention crisis before discussing acquisition.
Fail if: Agent jumps directly to paid ad strategy without flagging churn.
```

---

## shanks — Product Manager

### Critical

- [ ] **Working-backwards before spec:** For new features, writes press release / customer benefit before writing requirements
- [ ] **Non-goals explicit:** PRDs include what is NOT in scope
- [ ] **Outcomes not outputs:** Roadmaps specify business outcomes, not feature lists
- [ ] **Evidence-based:** Prioritization decisions reference data or customer quotes, not opinions

### Non-Critical

- [ ] Open questions explicitly flagged in PRDs
- [ ] Success metrics are specific and measurable
- [ ] Edge cases addressed in user stories
- [ ] Acceptance criteria are testable

### Test Prompts

```
Validation prompt 1 (non-goals check):
@shanks Write a PRD for a user notification system.

Expected: "Non-goals" section explicitly present.
Pass if: Explicit non-goals section with at least one item.
Fail if: No non-goals section.
```

```
Validation prompt 2 (outcomes check):
@shanks Build a product roadmap for Q3.

Expected: Outcomes expressed as business results, not feature names.
Pass if: Roadmap shows desired outcomes (e.g., "reduce churn from X to Y").
Fail if: Roadmap is a feature list (e.g., "Build notification system, redesign dashboard").
```

---

## killua — Orchestrator

### Critical

- [ ] **Acceptance criteria before assignment:** Every task assigned to a subagent includes explicit acceptance criteria
- [ ] **Parallel tracks identified:** When tasks are independent, they are flagged for parallel execution
- [ ] **higuruma gate present:** Every plan includes a higuruma audit step before final delivery
- [ ] **Blockers escalated:** Blockers are surfaced immediately, not buried in status updates

### Non-Critical

- [ ] Status updates use the standard format (✅/🔄/⏳/🚫)
- [ ] Dependencies are explicit in the plan
- [ ] Agent routing matches the routing table in ROUTING_RULES.md
- [ ] Plans account for the top 3 risks upfront

### Test Prompts

```
Validation prompt 1 (acceptance criteria check):
@killua Plan the launch of a new pricing page.

Expected: Each task includes acceptance criteria.
Pass if: Every assigned task has a "done when..." or equivalent criteria.
Fail if: Tasks are vague ("hisoka: design the page") without criteria.
```

```
Validation prompt 2 (higuruma gate check):
@killua Plan a sprint to build a checkout flow.

Expected: higuruma appears in the plan as a gate before delivery.
Pass if: higuruma explicitly assigned to audit before "done."
Fail if: Plan ends at toji's implementation without an audit step.
```

---

## Regression Testing

Run after any agent definition change:

1. Run all **Critical** checks for the modified agent
2. Run all **System-Level Critical** checks
3. Run the standard multi-agent workflow from `examples/multi-agent/README.md` Workflow 1 (abbreviated)
4. Confirm no regressions in adjacent agents (changes to killua routing could affect all agents)

Document results:

```
Regression Test Run
Date: [date]
Agent modified: [name]
Change: [description]
Critical checks: [pass/fail count]
Non-critical checks: [pass/fail count]
Regressions found: [yes/no — describe if yes]
Sign-off: [higuruma APPROVED / BLOCKED]
```
