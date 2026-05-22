# Agent Cheat Sheet

Fast routing. Pick by output artifact, not by keyword noise.

## Core Routes

| Need | Agent | Why |
|---|---|---|
| Code, build, fix, debug | `toji` | Produces working software |
| UI, UX, visual design, brand | `hisoka` | Produces visual spec and front-end craft |
| Research, market, investigate | `gon` | Produces sourced analysis |
| Copy, docs, email, writing | `yuji` | Produces text artifact |
| Audit, QA, verify, sign off | `higuruma` | Final quality gate |
| Infra, deploy, CI/CD, cloud | `pain` | Produces platform change |
| SQL, metrics, dashboard, cohort | `sukuna` | Produces data analysis |
| Growth, CRO, GTM, acquisition | `grimmjow` | Produces growth strategy |
| PRD, roadmap, user stories | `shanks` | Produces product spec |
| Multi-step project coordination | `killua` | Produces plan and routing |

## One-Line Rules

- If output is code, use `toji`.
- If question is "does it look right?", use `hisoka`.
- If source is external, use `gon`.
- If output is prose, use `yuji`.
- If output is quality verdict, use `higuruma`.
- If output is infra state change, use `pain`.
- If output is metrics or SQL, use `sukuna`.
- If output is growth plan, use `grimmjow`.
- If output is product spec, use `shanks`.
- If output is execution plan across agents, use `killua`.

## Gate Order

1. Build with specialist agent.
2. Audit with `higuruma`.
3. Ship only after audit passes.

