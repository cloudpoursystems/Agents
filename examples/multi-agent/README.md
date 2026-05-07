# Multi-Agent Orchestration Workflows

Five complete orchestration workflows showing how agents collaborate on complex projects. Each includes an agent handoff map, execution sequence, and prompt templates.

---

## Workflow 1: New Product Feature Launch

**Scenario:** Launch a new feature (e.g., "automated pour cost alerts") end-to-end.  
**Duration:** 1–2 weeks  
**Agents:** killua → gon + shanks (parallel) → hisoka + yuji (parallel) → toji → pain → higuruma

### Agent Handoff Map

```
killua
  ├── gon: research competitors' alert features
  └── shanks: write PRD for the feature
        ↓ (both complete)
  ├── hisoka: design the alert UI + settings screen
  └── yuji: write feature announcement email + in-app copy
        ↓ (both complete)
  toji: implement the feature
        ↓
  pain: deploy to staging
        ↓
  higuruma: full audit (code + design + copy)
        ↓
  pain: deploy to production
```

### Prompts

**Step 1 — killua (kickoff):**
```
@killua Plan and execute the launch of our new "automated pour cost alerts" feature.

Feature brief: Managers receive real-time alerts (email + in-app) when their 
pour cost % exceeds a configurable threshold. Target launch: 2 weeks.

Agents available: gon, shanks, hisoka, yuji, toji, pain, higuruma

Create: dependency map, agent assignments, parallel tracks, and 
day-by-day plan. Then kick off the parallel first tracks.
```

**Step 2a — gon (parallel):**
```
@gon Research how our top 5 competitors handle cost alerting:
- Do they have real-time alerts?
- What alert types and thresholds do they support?
- What do customers complain is missing?
- Any UX patterns we should reference or avoid?

Deliver findings for shanks to use in the PRD.
```

**Step 2b — shanks (parallel):**
```
@shanks Write a PRD for automated pour cost alerts.

Context from gon's research: [attach when ready, or run after gon]
User problem: Managers only discover pour cost problems at month-end.
Solution: Configurable threshold alerts via email and in-app.

Follow working-backwards format. Include: success metrics, user stories 
(manager persona + admin persona), requirements, edge cases (what if 
threshold is set too low? What if alert is triggered 100x/day?), open questions.
```

**Step 3a — hisoka (parallel, after PRD):**
```
@hisoka Design the UI for pour cost alerts.

PRD: [attach shanks output]
Screens needed:
1. Alert settings screen (threshold configuration, notification preferences)
2. In-app alert banner/toast component
3. Alert history list view
4. Email alert template

Constraints: Must fit our existing design system. Dark mode. Mobile responsive.
Deliver: HTML/CSS implementation of all components.
```

**Step 3b — yuji (parallel, after PRD):**
```
@yuji Write all copy for the pour cost alerts feature launch.

PRD: [attach shanks output]

Deliverables:
1. In-app copy: alert messages (5 variants by severity), settings labels, 
   empty state, error states
2. Feature announcement email to existing customers
3. In-app announcement modal copy
4. Help doc outline (1 page)

Voice: Direct, professional, hospitality-industry-literate. No jargon.
```

**Step 4 — toji (after design + copy):**
```
@toji Implement the automated pour cost alerts feature.

PRD: [attach]
Design: [attach hisoka output]
Copy: [attach yuji output]

Technical scope:
- Alert evaluation service (runs on transaction write)
- Alert preference storage (user settings)
- Email delivery integration (SendGrid)
- In-app notification storage and retrieval API
- Frontend components per design

TDD. Full test coverage for the alert evaluation logic.
```

**Step 5 — higuruma (final gate):**
```
@higuruma Full audit before we deploy this feature to production.

Audit all of:
1. toji's implementation — security, correctness, test coverage, performance
2. hisoka's design — accessibility, states, responsive, dark mode
3. yuji's copy — accuracy, clarity, consistency with brand voice

P0/P1/P2 findings. Block release on any P0.
```

---

## Workflow 2: SEO Content Engine

**Scenario:** Build a repeatable SEO content pipeline producing 4 articles/month.  
**Duration:** 2 weeks setup, then ongoing  
**Agents:** grimmjow → gon → yuji → higuruma

### Agent Handoff Map

```
grimmjow: keyword strategy + content calendar
    ↓
gon: research each target keyword (one article at a time)
    ↓
yuji: write the article from gon's research brief
    ↓
higuruma: content audit (factual accuracy, logic, strategic fit)
    ↓
yuji: revisions
    ↓
pain: deploy (if CMS needs technical publishing)
```

### Prompts

**Step 1 — grimmjow (strategy):**
```
@grimmjow Build our SEO content strategy for the next quarter.

Business: Cloud Pour — beverage management software for hospitality
ICP: F&B directors at hotels and restaurant groups
Current organic traffic: ~800/month
Goal: 3,000/month in 90 days

Deliver:
1. Top 20 target keywords (with search volume, difficulty, intent)
2. Content calendar for 12 articles
3. Cluster map (which articles support which pillar pages)
4. Internal linking plan
5. Success metrics we'll track
```

**Step 2 — gon (per article):**
```
@gon Research brief for article: "[target keyword]"

Target keyword: [from grimmjow's calendar]
Search intent: [informational / transactional / navigational]
Target reader: [ICP description]

Research needed:
1. What do the top 5 ranking articles cover?
2. What questions do people ask on Reddit/forums about this topic?
3. What data and statistics are available to cite?
4. What's the best angle that isn't well-covered?

Deliver: Research brief with outline recommendation, key data points, 
recommended sources, and angle recommendation.
```

**Step 3 — yuji (per article):**
```
@yuji Write an SEO article for: "[target keyword]"

Research brief from gon: [attach]
Target length: 1,800–2,200 words
Target reader: F&B director with this problem
Content goal: Rank #1 for the keyword; secondary goal is demo intent

Requirements:
- Search intent satisfied in first 2 paragraphs
- Practical, specific — no vague advice
- 3+ original frameworks or step-by-step processes
- Statistics cited with links
- Soft CTA to Cloud Pour in final section only (not salesy)
- Meta title + meta description included
```

**Step 4 — higuruma (audit):**
```
@higuruma Audit this SEO article before publication.

[attach yuji's draft]

Check:
1. Every statistic — is it real, current, and correctly attributed?
2. Every claim — is it accurate and supportable?
3. Logic — does the argument flow? Any unsupported leaps?
4. Strategic — could any claim create reputational risk?
5. SEO — does it satisfy the search intent?
```

---

## Workflow 3: Growth Experiment Sprint

**Scenario:** Run a structured growth experiment — identify lever, design test, analyze results.  
**Duration:** 4 weeks (1 design, 2 running, 1 analysis)  
**Agents:** sukuna → grimmjow → toji → sukuna → grimmjow

### Agent Handoff Map

```
sukuna: analyze funnel — where is the biggest drop-off?
    ↓
grimmjow: design A/B test for the identified leak
    ↓
toji: implement the variant
    ↓
higuruma: review variant before launch
    ↓
[test runs 2 weeks]
    ↓
sukuna: analyze results + statistical significance
    ↓
grimmjow: decide ship/kill + next experiment
```

### Prompts

**Step 1 — sukuna (funnel analysis):**
```
@sukuna Analyze our signup-to-activation funnel and identify the biggest drop-off.

Tables available:
- signups(id, created_at, source, plan_selected)
- onboarding_events(user_id, step, completed_at)
- activations(user_id, activated_at) -- "activated" = connected first POS

Steps in funnel:
1. Signup → email verified
2. Email verified → onboarding started
3. Onboarding started → POS connected
4. POS connected → first report generated (activation)

Deliver: Drop-off % at each step, cohort comparison by signup source, 
and your top 2 hypotheses for what's causing the biggest leak.
```

**Step 2 — grimmjow (test design):**
```
@grimmjow Design an A/B test to address the funnel drop-off sukuna identified.

Analysis from sukuna: [attach]
Top hypothesis: [from sukuna's findings]

Design the test:
1. Hypothesis: if we [change X], then [metric Y] will improve because [reason]
2. Variant description: exactly what changes?
3. Success metric: primary + secondary (guardrail metrics)
4. Sample size needed for 80% power at p<0.05
5. Test duration
6. Risks: what could this break?
```

**Step 3 — toji (implementation):**
```
@toji Implement this A/B test variant.

Test design from grimmjow: [attach]
Variant: [specific UI/copy/flow changes]

Requirements:
- Use our existing A/B test framework ([framework name])
- 50/50 split, randomized by user_id
- Track all required events to sukuna's spec
- No changes to control group — variant only adds/modifies
- Feature flag so we can kill it instantly

Deliver: Implementation + event tracking code + rollback procedure.
```

**Step 4 — sukuna (results analysis):**
```
@sukuna Analyze the A/B test results.

Test: [name from grimmjow's design]
Duration: 14 days
Control group: [N] users
Variant group: [N] users

Raw data: [attach or describe where to query]

Deliver:
1. Statistical significance (p-value, confidence interval)
2. Effect size (absolute and relative lift)
3. Segment breakdown (did it work better for certain user types?)
4. Secondary metric impact (did we hurt anything?)
5. Recommendation: ship, kill, or iterate?
```

---

## Workflow 4: Technical Debt Paydown

**Scenario:** Address accumulated technical debt before it becomes a production risk.  
**Duration:** 1–2 weeks  
**Agents:** toji → higuruma → toji → pain

### Agent Handoff Map

```
toji: audit codebase for technical debt
    ↓
higuruma: prioritize findings by risk + impact
    ↓
toji: fix P0 and P1 items
    ↓
higuruma: verify fixes + sign off
    ↓
pain: deploy + monitor
```

### Prompts

**Step 1 — toji (debt audit):**
```
@toji Audit the codebase for technical debt. Produce a prioritized list.

Areas to check:
1. Security: outdated dependencies, auth gaps, injection vectors
2. Performance: N+1 queries, missing indexes, memory leaks
3. Reliability: error handling gaps, missing retries, no circuit breakers
4. Maintainability: files >300 lines, functions >20 lines, missing tests
5. Observability: unlogged errors, missing metrics, no health checks

Repo: [describe or list key files]
Output: Findings table with severity (P0/P1/P2), file:line, description, 
estimated fix time.
```

**Step 2 — toji (fixes):**
```
@toji Fix all P0 and P1 items from the debt audit.

Audit findings: [attach]

For each fix:
1. Write a test that captures the problem first
2. Implement the minimum fix
3. Verify the test passes
4. Note any risk in the fix (rollback procedure if needed)

Do NOT fix P2 items — log them as issues for later.
```

---

## Workflow 5: Quarterly Business Review Prep

**Scenario:** Prepare a full QBR presentation — metrics, analysis, strategy.  
**Duration:** 3–5 days  
**Agents:** sukuna → gon → shanks → yuji → higuruma

### Agent Handoff Map

```
sukuna: pull and analyze all Q metrics
    ↓
gon: research market context (industry trends, competitor moves)
    ↓
shanks: synthesize into product strategy narrative + roadmap update
    ↓
yuji: write the QBR deck narrative + executive summary
    ↓
higuruma: fact-check all numbers + logic audit
    ↓
yuji: final revisions
```

### Prompts

**Step 1 — sukuna (metrics package):**
```
@sukuna Pull our complete Q[N] metrics package for the QBR.

Metrics needed:
- Revenue: MRR start/end, new MRR, churned MRR, expansion MRR, growth rate
- Customers: new customers, churned, net adds, total
- Retention: logo retention, net revenue retention
- Unit economics: CAC by channel, LTV, payback period
- Product: DAU/MAU, activation rate, feature adoption rates
- Pipeline: leads, trials, trial-to-paid conversion

Format: Slide-ready numbers with QoQ and YoY comparisons.
Flag any metrics that look anomalous and your hypothesis why.
```

**Step 2 — gon (market context):**
```
@gon Research the external context for our Q[N] QBR.

We need: 
1. What happened in our market this quarter? (competitor moves, funding, launches)
2. Any macro trends affecting hospitality/F&B spend?
3. What are customers in our space talking about? (review sites, forums, LinkedIn)
4. Any regulatory or technology shifts we should flag?

Deliver: 1-page market snapshot with the 5 most relevant developments 
and their implications for our strategy.
```

**Step 3 — shanks (strategy narrative):**
```
@shanks Write the strategic narrative for our Q[N] QBR.

Metrics from sukuna: [attach]
Market context from gon: [attach]

Deliver:
1. Q[N] performance summary (what we set out to do vs. what happened)
2. Learnings (3 most important things we learned)
3. Q[N+1] strategic bets (3 priorities with rationale)
4. Updated roadmap (outcome-based, not feature list)
5. Resource needs or asks (if any)
```

**Step 4 — yuji (QBR deck copy):**
```
@yuji Write the QBR deck copy.

Strategy narrative from shanks: [attach]
Metrics package from sukuna: [attach]

Audience: Board members and investors (not day-to-day operators)
Length: 15–20 slides
Tone: Confident, honest, forward-looking — not spin

Deliver: Slide-by-slide copy (headline + 3 bullets max per slide). 
Include: executive summary (1 slide), metrics dashboard (2–3 slides), 
narrative (8–10 slides), ask/next quarter (2 slides).
```

**Step 5 — higuruma (fact check):**
```
@higuruma Fact-check the QBR deck before it goes to the board.

Deck: [attach yuji output]
Source data from sukuna: [attach]

Check every number: Does each metric in the deck match sukuna's source data?
Check logic: Do the conclusions follow from the data presented?
Check strategic claims: Are the market assertions supported by gon's research?

P0 = wrong number or unsupported claim (must fix)
P1 = unclear or misleading framing (should fix)
P2 = polish improvements (optional)
```
