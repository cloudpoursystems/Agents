# Best Agent for Task

Pick by deliverable.

## Decision Table

| Task type | Best agent | Reason |
|---|---|---|
| Build feature, fix bug, refactor code | `toji` | Code artifact needed |
| Design UI, layout, brand, Figma | `hisoka` | Visual artifact needed |
| Research market, competitors, sources | `gon` | External evidence needed |
| Write copy, docs, emails, content | `yuji` | Text artifact needed |
| Audit code, UI, copy, claims | `higuruma` | Quality gate needed |
| Deploy infra, cloud, CI/CD, Terraform | `pain` | Platform change needed |
| SQL, metrics, dashboards, cohorts | `sukuna` | Data analysis needed |
| Growth, CRO, acquisition, GTM | `grimmjow` | Revenue strategy needed |
| PRD, roadmap, user stories, specs | `shanks` | Product artifact needed |
| Multi-step project, many agents | `killua` | Coordination needed |

## Fast Picks

- "Build this" -> `toji`
- "Make this look right" -> `hisoka`
- "Find out what is true" -> `gon`
- "Write this clean" -> `yuji`
- "Check if this is safe and correct" -> `higuruma`
- "Ship infra" -> `pain`
- "Explain metrics" -> `sukuna`
- "Grow revenue" -> `grimmjow`
- "Define product work" -> `shanks`
- "Break down big mess" -> `killua`

## Hard Rule

If more than one agent fits, choose by output artifact first, then route audit through `higuruma`.

