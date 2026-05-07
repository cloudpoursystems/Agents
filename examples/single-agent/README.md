# Single-Agent Prompt Examples

Ready-to-use prompt examples for each of the 10 agents. Copy, adapt, and use directly in Claude Code.

---

## toji — Software Engineer

### Build a new feature
```
@toji Build a user authentication system with:
- JWT-based auth (access + refresh tokens)
- Email/password signup and login
- Password reset via email
- Rate limiting on auth endpoints
- Tests for all paths including edge cases

Stack: Node.js/TypeScript, Express, PostgreSQL
```

### Debug a production issue
```
@toji Debug this production error:

Error: Cannot read properties of undefined (reading 'id')
  at getUserProfile (src/users/profile.ts:47)
  
Here's the relevant code:
[paste code]

This only happens for users who signed up via Google OAuth, not email. 
Trace the execution path and identify root cause.
```

### Refactor for performance
```
@toji This endpoint takes 4.2 seconds to respond. Profile it and fix the performance issue.

[paste code]

Database: PostgreSQL with 2M user records.
Target: <200ms p95.
```

### Build an MCP server
```
@toji Build an MCP server in TypeScript that exposes these tools:
1. search_documents(query: string) — full-text search over our document store
2. get_document(id: string) — fetch a specific document
3. create_document(title: string, content: string) — create a new document

Use the MCP SDK. Include proper error handling and input validation.
```

### Code review
```
@toji Review this PR before I merge it:

[paste diff or link to PR]

Focus on: security vulnerabilities, logic errors, missing edge cases, 
performance issues. Use P0/P1/P2 severity.
```

---

## hisoka — Designer

### Design a landing page section
```
@hisoka Design a hero section for a SaaS product landing page.

Product: Cloud Pour — beverage program management for hospitality venues
Audience: F&B directors at hotels and restaurants
Goal: Drive demo requests
Brand: Premium, minimal, hospitality-forward

Deliver: Complete HTML/CSS with dark and light mode, mobile-first, 
all interactive states. Use OKLCH colors and CSS custom properties.
```

### Design a component
```
@hisoka Design a pricing card component with:
- Monthly/annual toggle
- Three tiers: Starter, Pro, Enterprise
- Feature comparison list
- CTA button per tier
- "Most popular" badge variant

Constraints: Must meet WCAG AA, mobile responsive, dark mode.
Deliver as self-contained HTML/CSS.
```

### Brand identity
```
@hisoka Create a brand identity system for:

Company: Meridian Analytics
Industry: B2B data platform
Positioning: Precise, trustworthy, sophisticated — not cold or corporate
Audience: Data engineers and analytics leaders

Deliver: Color palette (OKLCH), typography scale, spacing system, 
logo concept direction, and CSS custom property token file.
```

### Implement a Figma design
```
@hisoka Implement this Figma design as production HTML/CSS:

[Figma URL]

Requirements:
- Pixel-perfect implementation
- Mobile responsive (320px to 1920px)
- Dark mode support
- WCAG AA minimum
- Use the design tokens from our existing theme
```

### Elevate existing UI
```
@hisoka This UI feels flat and generic. Elevate it without changing the layout or functionality.

[paste HTML/CSS or screenshot path]

The brand is: [describe brand]
What's wrong: lack of visual hierarchy, inconsistent spacing, weak typography
```

---

## gon — Researcher

### Market research
```
@gon Research the event management software market:

1. Who are the top 10 players and their positioning?
2. What is the total addressable market?
3. What pricing models dominate?
4. What are the most common customer complaints (from reviews, forums)?
5. What whitespace exists in the market?

Deliver: Executive summary, confidence ratings for each finding, 
source quality grades, and implications for product strategy.
```

### Competitive intelligence
```
@gon Deep-dive competitive analysis on Linear (linear.app):

- Product: core features, recent launches, roadmap signals
- Pricing: model, tiers, enterprise approach
- Marketing: positioning, messaging, channels
- Growth: estimated ARR, team size, funding
- Weaknesses: what do users complain about?

Sources: their website, app, G2/Capterra reviews, Twitter, 
Hacker News threads, job postings (signals intent).
```

### User research synthesis
```
@gon Synthesize these 15 customer interview transcripts and identify:

1. Top 3 jobs-to-be-done
2. Most common pain points (ranked by frequency)
3. Current alternatives they use
4. Language they use to describe their problem (for copy)
5. Buying triggers and blockers

[attach transcripts or paste content]
```

### Tech ecosystem analysis
```
@gon Analyze the developer tooling market for AI-native developer tools:

- Which categories are emerging?
- Who are the funded players in each?
- What's the adoption curve look like?
- What are developers asking for that doesn't exist yet?

Use developer communities (HN, Reddit, Twitter, GitHub issues) as sources.
```

---

## yuji — Writer

### Landing page copy
```
@yuji Write the full copy for our SaaS landing page.

Product: Cloud Pour — beverage program management platform for hospitality
ICP: F&B directors at hotels (200+ rooms) and restaurant groups (3+ locations)
Core pain: Manual beverage cost tracking, inconsistent pours, margin leakage
Core benefit: Real-time pour cost visibility and team accountability
CTA: Book a demo

Deliver: Hero headline + subhead, 3 benefit sections, social proof section, 
FAQ section, and CTA section. One CTA throughout: book demo.
```

### Email sequence
```
@yuji Write a 5-email onboarding sequence for new trial signups.

Product: [product name]
Trial length: 14 days
Goal: Get users to [key activation event] within first 3 days

Email 1: Sent immediately — welcome + first action
Email 2: Day 1 — help them complete setup
Email 3: Day 3 — value reinforcement / "aha moment" nudge
Email 4: Day 7 — social proof + feature spotlight
Email 5: Day 12 — trial ending + conversion offer

Tone: Direct, helpful, zero fluff.
```

### Blog post
```
@yuji Write a 2,000-word SEO blog post targeting: "beverage cost control restaurant"

Research brief from gon: [attach or paste]
Target reader: Restaurant owner or F&B director struggling with beverage margins
Angle: Practical, data-backed guide — not a sales pitch
Include: 3 actionable frameworks they can use today
CTA at end: soft mention of Cloud Pour as one solution

Requirements: Search intent first, no filler, no "innovative solutions" language.
```

### Internal announcement
```
@yuji Write an internal announcement for the company about this product decision:

Decision: We're sunsetting our mobile app and going web-only
Why: Mobile accounted for 3% of usage, 40% of engineering cost
Impact: Current mobile users will migrate to web
Timeline: App deprecated in 60 days

Audience: 45-person team, some are surprised, some knew it was coming
Tone: Honest, confident, not apologetic
```

---

## higuruma — Quality Auditor

### Full code audit
```
@higuruma Audit this codebase before we ship to production.

[paste code or describe what to read]

Specifically check:
1. Authentication and authorization — are all endpoints protected correctly?
2. Input validation — is everything from external sources sanitized?
3. Error handling — are failures handled gracefully everywhere?
4. SQL queries — any injection risks?
5. Test coverage — what critical paths aren't tested?

Output: Prioritized findings (P0/P1/P2) with specific file and line references.
```

### Design quality review
```
@higuruma Audit this UI before it goes to staging.

[paste HTML/CSS or screenshot paths]

Check:
- WCAG AA compliance (color contrast, keyboard nav, focus states)
- All interactive states (hover, focus, active, disabled, loading, error)
- Mobile responsiveness at 320px, 768px, 1280px
- Dark mode correctness
- Brand consistency with our design system
```

### Copy review
```
@higuruma Review this landing page copy before it goes live.

[paste copy]

Check:
- Every specific claim (stats, percentages) — are they sourced and accurate?
- Logic: does the argument hold? Any unsupported leaps?
- Strategic: could any claim create legal or reputational risk?
- Clarity: anything that requires re-reading?
```

---

## pain — DevOps Engineer

### Terraform infrastructure
```
@pain Write Terraform for a production-grade web application on AWS:

- ECS Fargate cluster for the API (2 tasks minimum, auto-scaling to 10)
- RDS PostgreSQL (Multi-AZ, encrypted at rest)
- ElastiCache Redis for session storage
- ALB with SSL termination
- VPC with public/private subnets
- WAF rules for the ALB
- CloudWatch alarms for CPU, memory, error rate

Include: State management in S3, outputs file, rollback procedure.
```

### CI/CD pipeline
```
@pain Set up a GitHub Actions pipeline for a Node.js/TypeScript API:

Triggers: PR (test only), merge to main (test + deploy to staging), 
manual (deploy to production)

Pipeline stages:
1. Lint and type check
2. Unit tests
3. Integration tests (with DB)
4. Build Docker image and push to ECR
5. Deploy to ECS (staging auto, production manual approval)
6. Smoke test post-deploy
7. Rollback on failure

Security: Secrets via GitHub Environments, not hardcoded.
```

### Incident response
```
@pain Production incident:

Alert: Error rate spiked from 0.1% to 23% at 14:32 UTC
Service: API gateway
Recent changes: Deployed v2.4.1 at 14:28 UTC (diff: [paste or describe])
Metrics: [paste relevant Datadog/CloudWatch data]

Walk me through: immediate containment, diagnosis steps, fix options, 
and what we'd put in the post-mortem.
```

---

## sukuna — Data Analyst

### SQL for business metrics
```
@sukuna Write SQL to calculate our 30/60/90 day cohort retention.

Tables:
- users(id, created_at, plan)
- events(user_id, event_type, created_at)

Definition of "retained": user logged in at least once in the period
Cohort: monthly signup cohorts
Output: retention matrix by cohort and period, plus aggregate retention curve
Database: PostgreSQL
```

### A/B test analysis
```
@sukuna Analyze this A/B test result:

Test: New onboarding flow vs. control
Duration: 14 days
Control: 4,231 users — 23.4% completed activation
Variant: 4,189 users — 27.1% completed activation

Tell me: Is this statistically significant? What's the effect size? 
What's the expected annual revenue impact if we ship it?
(Assume: 1,000 new users/week, $99/mo ARPU, 12-month LTV)
```

### Build a dashboard
```
@sukuna Design the metrics dashboard for our weekly business review.

Audience: CEO, CTO, Head of Growth (non-technical)
Key questions they ask every week:
1. Are we growing?
2. Are we keeping customers?
3. Is our unit economics improving?

Metrics to include: MRR, MRR growth, new MRR, churned MRR, expansion MRR, 
trial starts, trial-to-paid conversion, DAU/MAU, NPS.

Deliver: Dashboard layout spec, SQL for each metric, refresh cadence.
```

---

## grimmjow — Growth Strategist

### Growth strategy
```
@grimmjow We're at $180K MRR, growing 8% MoM. Growth is slowing.

Current: 
- 60% of new customers from word-of-mouth
- CAC: $420, LTV: $2,800, payback: 8 months
- Top churn reasons: "too complex" (42%), "price" (28%), "missing feature X" (18%)

Build me: A 90-day growth plan to get back to 15% MoM growth.
Constraints: $25K/month marketing budget, 2-person growth team.
```

### Landing page conversion audit
```
@grimmjow Audit our landing page for conversion problems.

URL: [paste content or describe page]
Current conversion rate: 2.1% visitor-to-trial
Industry benchmark: ~4-6% for our category
Traffic sources: 55% SEO, 30% paid, 15% direct

Identify: The top 3 conversion killers and specific fixes for each.
Prioritize by: Expected impact on conversion rate.
```

### Email drip strategy
```
@grimmjow Design a lead nurture email sequence for marketing-qualified leads 
who downloaded our ROI calculator but didn't start a trial.

Lead profile: F&B director, 2-10 location restaurant group, indicated 
beverage cost is a problem
Sequence goal: Get them to book a demo within 21 days
Touches: 5 emails max

For each email: subject line, goal, key message, CTA.
Then hand off the writing to yuji.
```

---

## shanks — Product Manager

### Write a PRD
```
@shanks Write a PRD for a new feature: automated pour cost alerts.

Context: We're building beverage management software for restaurants.
Problem: Managers don't know their pour cost is off until month-end.
Solution: Real-time alerts when pour cost % exceeds threshold.

Follow Amazon working-backwards format. Include: problem statement, 
success metrics, non-goals, user stories, requirements, edge cases, 
open questions, launch plan.
```

### Build a roadmap
```
@shanks Build a Q3 outcome-based roadmap.

Team: 4 engineers, 1 designer
Current state: [describe]
Top 3 bets for the quarter: 
1. Reduce churn from "too complex" (affects 42% of churned customers)
2. Expand to wine programs (currently beer-only)
3. API for POS integrations (requested by 12 enterprise prospects)

Prioritize using RICE. Show: outcome per initiative, risks, dependencies.
```

### Discovery interview script
```
@shanks Write a discovery interview script for talking to restaurant F&B directors 
about their beverage program management pain.

Goal: Understand their current workflow, tools, frustrations, and what 
"better" looks like to them. Do NOT pitch our product.
Duration: 30 minutes
Framework: Jobs-to-be-Done

Include: Opener, context-setting questions, JTBD deep-dive, current tools 
audit, wrap-up. Add interviewer notes on what to listen for.
```

---

## killua — Orchestrator

### Full product launch
```
@killua Orchestrate a full product launch for our new wine program feature.

Launch target: 3 weeks from now
Team: toji (eng), hisoka (design), yuji (copy), gon (research), higuruma (QA)

Deliverables needed:
- Competitive research on wine management features
- Updated landing page section
- Feature announcement email to existing customers  
- In-app announcement
- Implementation of the feature
- Quality audit of everything before launch

Create: A dependency map, agent assignment table, parallel tracks, 
and day-by-day execution plan.
```

### Debug a complex problem
```
@killua Coordinate investigation of this production issue across the team:

Symptom: Checkout conversion dropped from 71% to 54% this week
No recent deploys
Metrics look normal (latency, error rate)

Assign:
- sukuna: analyze conversion funnel data to isolate where drop-off happens
- toji: review code for any silent failures in the checkout flow
- gon: check if this is a known industry problem (seasonality? payment processor issue?)

Synthesize findings and propose a fix.
```
