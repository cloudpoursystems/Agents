# Routing Rules

Decision logic for selecting the right agent, resolving overlaps, and composing multi-agent workflows.

---

## Primary Routing Table

Match the **intent** of the request to the agent's core domain.

| Request type | Agent | Decision signal |
|-------------|-------|-----------------|
| Write, build, fix, refactor code | **toji** | Any code artifact as output |
| Design UI, landing page, brand | **hisoka** | Visual/HTML/CSS as output |
| Research, investigate, analyze market | **gon** | Synthesis of external information |
| Write copy, blog, email, docs | **yuji** | Prose/text artifact as output |
| Audit, review, verify anything | **higuruma** | Quality assessment as output |
| Deploy, configure infra, CI/CD | **pain** | Infrastructure state as output |
| SQL, metrics, dashboards, A/B | **sukuna** | Data/quantitative insight as output |
| Growth, CRO, GTM, paid ads | **grimmjow** | Revenue/acquisition strategy as output |
| PRD, roadmap, user stories, OKR | **shanks** | Product spec as output |
| Multi-step project coordination | **killua** | Agent-orchestrated plan as output |

---

## Overlap Resolution

### toji vs hisoka (code vs design)

| Situation | Correct agent |
|-----------|--------------|
| Building a React component from scratch | toji (code output) |
| Designing the visual spec for a component | hisoka (design output) |
| Implementing an existing Figma design | toji |
| Reviewing a Figma design for accuracy | hisoka |
| Writing CSS with creative visual decisions | hisoka |
| Writing CSS to implement specified styles | toji |

**Rule:** If the open question is "does it look right?", use hisoka. If "does it work?", use toji.

### gon vs sukuna (research vs data)

| Situation | Correct agent |
|-----------|--------------|
| Market sizing of a new category | gon (external research) |
| Calculating current user LTV from DB | sukuna (internal data) |
| Competitive intelligence on a rival | gon |
| Cohort retention analysis | sukuna |
| Finding industry benchmark metrics | gon |
| Building a metrics dashboard | sukuna |

**Rule:** If the source is external (web, reports, interviews), use gon. If internal (database, product analytics), use sukuna.

### yuji vs grimmjow (writing vs growth)

| Situation | Correct agent |
|-----------|--------------|
| Writing landing page copy | yuji |
| Designing the conversion strategy for a landing page | grimmjow |
| Writing an email | yuji |
| Designing an email drip sequence strategy | grimmjow |
| Writing blog posts | yuji |
| SEO keyword strategy and content planning | grimmjow |

**Rule:** If the output is a text artifact, use yuji. If the output is a strategy/plan for revenue impact, use grimmjow. For an SEO article, grimmjow plans → yuji writes.

### shanks vs killua (PM vs orchestrator)

| Situation | Correct agent |
|-----------|--------------|
| Writing a PRD | shanks |
| Planning a multi-agent project execution | killua |
| Sprint planning | shanks |
| Coordinating toji + hisoka + gon on a launch | killua |
| OKR definition | shanks |
| Breaking down a large ambiguous goal | killua |

**Rule:** shanks produces product artifacts. killua produces execution plans and routes to agents.

### pain vs toji (infra vs code)

| Situation | Correct agent |
|-----------|--------------|
| Writing Terraform for a new AWS service | pain |
| Writing backend application code | toji |
| Setting up a GitHub Actions CI pipeline | pain |
| Writing the code that runs inside CI | toji |
| Debugging a Kubernetes crash | pain |
| Debugging an application crash | toji |

**Rule:** If it's infrastructure-as-code or platform operations, use pain. If it's application code, use toji.

---

## Workflow Patterns

### Pattern 1: Research → Write

```
gon (research) → yuji (write)
```

Use when: blog post, thought leadership, market analysis report, competitive brief.

Example:
```
gon: Research the current state of event management software — key players, pricing, positioning gaps
yuji: Write a 2,000-word SEO article targeting "event management software" using gon's research
```

### Pattern 2: Design → Build → Audit

```
hisoka (design) → toji (build) → higuruma (audit)
```

Use when: new UI feature, landing page, component library addition.

Example:
```
hisoka: Design the pricing page — tokens, layout, dark/light, all states
toji: Implement the pricing page from hisoka's design
higuruma: Audit for accessibility, correctness, edge cases
```

### Pattern 3: Research → Spec → Build → Audit

```
gon (research) → shanks (PRD) → toji (build) → higuruma (audit)
```

Use when: building a new product feature with discovery needed first.

### Pattern 4: Data → Growth Strategy → Copy

```
sukuna (analyze) → grimmjow (strategy) → yuji (copy)
```

Use when: retention problem → fix strategy → write the emails/in-app messages.

### Pattern 5: Full Launch

```
killua orchestrates:
  ┌─ gon: competitive research
  ├─ sukuna: analyze current funnel
  └─ shanks: GTM spec
        ↓
  ┌─ hisoka: design
  └─ yuji: copy
        ↓
  toji: implement
        ↓
  pain: deploy
        ↓
  higuruma: final audit
```

---

## Escalation Rules

### When to use killua

Use killua when:
- The task spans more than 2 agents
- The order of operations is non-obvious
- There are parallel tracks that need coordination
- A blocker in one track affects others

Do **not** use killua when a single specialist can handle the full task.

### higuruma gate rule

**Always** route to higuruma before final delivery when:
- Code ships to production
- Copy goes to a public surface
- Infrastructure changes are applied
- Data analysis informs a high-stakes decision

Higuruma is non-optional for P0 deliverables.

---

## Anti-Patterns

- **Don't use killua for simple tasks.** If it's one agent, go direct.
- **Don't skip higuruma on production-bound work.** Quality debt compounds.
- **Don't split a single logical task across agents.** One agent owns one deliverable.
- **Don't route to gon when sukuna has the data.** Internal data = sukuna.
- **Don't ask yuji to strategize.** yuji executes writing, grimmjow designs strategy.
