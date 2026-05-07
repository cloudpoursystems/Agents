# Claude Agents

A team of 10 specialized Claude agents for the Claude Code platform. Each agent is a domain expert that routes tasks through the right skills and tools, producing top-tier output with zero generalist compromise.

## Architecture

```
                        ┌─────────────┐
                        │   killua    │
                        │ Orchestrator│
                        └──────┬──────┘
                               │ spawns & coordinates
          ┌────────────────────┼────────────────────┐
          │            ┌───────┴──────┐              │
     ┌────▼────┐  ┌────▼────┐  ┌─────▼────┐  ┌─────▼────┐
     │  toji   │  │ hisoka  │  │   gon    │  │  yuji    │
     │  Code   │  │ Design  │  │ Research │  │  Write   │
     └────┬────┘  └────┬────┘  └─────┬────┘  └─────┬────┘
          │            │             │              │
     ┌────▼────┐  ┌────▼────┐  ┌─────▼────┐  ┌─────▼────┐
     │  pain   │  │ shanks  │  │  sukuna  │  │grimmjow  │
     │  Infra  │  │   PM    │  │   Data   │  │  Growth  │
     └─────────┘  └─────────┘  └──────────┘  └──────────┘
                               
                        ┌─────────────┐
                        │  higuruma   │
                        │ Quality Gate│
                        └─────────────┘
```

Every deliverable passes through **higuruma** before shipping.

## The 10 Agents

| Agent | Domain | Model | Trigger keywords |
|-------|--------|-------|-----------------|
| [toji](toji.md) | Software engineering | opus-4-7 | code, build, feature, API, debug, fix, test |
| [hisoka](hisoka.md) | Design & UI/UX | opus-4-7 | design, UI, UX, CSS, HTML, layout, brand |
| [gon](gon.md) | Research & analysis | opus-4-7 | research, market, analyze, investigate, data |
| [yuji](yuji.md) | Writing & marketing copy | opus-4-7 | copy, blog, docs, email, write, content |
| [higuruma](higuruma.md) | Quality audit | opus-4-7 | audit, review, verify, QA, sign off |
| [pain](pain.md) | DevOps & infrastructure | opus-4-7 | deploy, infra, cloud, terraform, docker, CI/CD |
| [sukuna](sukuna.md) | Data & analytics | opus-4-7 | SQL, metrics, dashboard, cohort, A/B test |
| [grimmjow](grimmjow.md) | Growth & acquisition | opus-4-7 | growth, CRO, funnel, paid ads, GTM, retention |
| [shanks](shanks.md) | Product management | opus-4-7 | PRD, roadmap, user story, sprint, backlog |
| [killua](killua.md) | Orchestration | opus-4-7 | plan, coordinate, assign, orchestrate, project |

## Quick Start

### Single Agent

```
@toji Build a REST API endpoint for user authentication with JWT
```

```
@gon Research the top 5 competitors in the event-management SaaS space
```

```
@hisoka Design a landing page hero section with dark mode support
```

### Multi-Agent via Killua

```
@killua Plan and execute a full product launch:
- Competitor research (gon)
- Landing page copy (yuji)
- Landing page design (hisoka)
- Implementation (toji)
- Quality audit (higuruma)
```

## Repository Structure

```
claude-agents/
├── README.md               # This file
├── AGENT_INDEX.md          # Full agent profiles
├── ROUTING_RULES.md        # When to use which agent
├── INSTALLATION.md         # Setup and configuration
├── SKILL_REGISTRY.md       # All skills by agent
├── QUALITY_GATE.md         # Higuruma audit protocols
├── CHANGELOG.md            # Release history
├── examples/
│   ├── single-agent/       # Per-agent prompt examples
│   └── multi-agent/        # Orchestration workflows
├── tests/
│   └── VALIDATION_CHECKLIST.md
├── gon.md
├── grimmjow.md
├── higuruma.md
├── hisoka.md
├── killua.md
├── pain.md
├── shanks.md
├── sukuna.md
├── toji.md
└── yuji.md
```

## Design Principles

- **Specialist over generalist** — each agent is world-class in one domain
- **Skill-first** — agents invoke registered skills before starting work
- **Audit gate** — higuruma signs off every deliverable before delivery
- **Parallel execution** — killua runs independent tracks simultaneously
- **Explicit handoffs** — no implicit assumptions between agents

## Model

All agents run on `claude-opus-4-7` for maximum capability.
