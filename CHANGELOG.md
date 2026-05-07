# Changelog

All notable changes to the claude-agents system are documented here.

---

## [1.0.0] — 2026-05-07

### Initial Release

The first production release of the claude-agents system: 10 specialized agents for the Claude Code platform covering the full product development lifecycle.

### Agents Added

| Agent | Domain | Skills |
|-------|--------|--------|
| `toji` | Software engineering | 33 |
| `hisoka` | Design & UI/UX | 18 |
| `gon` | Research & analysis | 22 |
| `yuji` | Writing & content | 33 |
| `higuruma` | Quality audit | 18 |
| `pain` | DevOps & infrastructure | 16 |
| `sukuna` | Data & analytics | 12 |
| `grimmjow` | Growth & acquisition | 57 |
| `shanks` | Product management | 65 |
| `killua` | Orchestration | 10 |

### Documentation Added

- `README.md` — Architecture overview, agent table, quick start
- `AGENT_INDEX.md` — Full profiles for all 10 agents with triggers, strengths, and skill tables
- `ROUTING_RULES.md` — Decision logic, overlap resolution, workflow patterns
- `INSTALLATION.md` — Setup, Claude Code config, env vars, troubleshooting
- `SKILL_REGISTRY.md` — Every skill mapped by agent and by bundle
- `QUALITY_GATE.md` — Higuruma audit protocols, severity definitions, sign-off criteria
- `examples/single-agent/README.md` — Prompt examples for all 10 agents
- `examples/multi-agent/README.md` — 5 full orchestration workflows with agent handoff maps
- `tests/VALIDATION_CHECKLIST.md` — Per-agent critical and non-critical checks

### Architecture Decisions

**Why 10 agents?**  
The system covers every major function in a software product company: code, design, research, writing, quality, infrastructure, data, growth, product, and coordination. Each domain requires specialist depth that a generalist cannot provide at the required quality level.

**Why claude-opus-4-7?**  
All agents run on Opus 4.7 for maximum capability. The quality bar for each domain — production code, pixel-perfect design, rigorous research — requires the most capable model.

**Why skills?**  
Skills are reusable prompt modules that encode domain-specific workflows. Agents invoke skills via the `Skill` tool to get structured, repeatable processes rather than re-inventing the approach for each task.

**Why higuruma as the final gate?**  
Quality debt compounds. Catching a P0 at the design stage costs minutes. Catching it after deployment costs hours (or customers). A dedicated auditor who never ships their own work maintains objectivity.

---

## Roadmap

### [1.1.0] — Planned

- Add agent for legal/compliance review
- Add agent for customer support / success
- Expand `devops-skills:*` bundle coverage in pain
- Add `pm-toolkit:*` skills to shanks
- Cross-agent memory: shared context passing between agents in a session

### [1.2.0] — Planned

- Agent composition templates: pre-built killua plans for common workflows
- Skill performance tracking: which skills get invoked most, quality outcomes
- Agent-specific CLAUDE.md overlays: project-level overrides per agent

### [2.0.0] — Future

- Agent self-improvement: higuruma feedback loop writes back to agent prompts
- Dynamic routing: automatic agent selection based on task classification
- Skill marketplace: community-contributed skill bundles

---

## Migration Guide

### From no agents (manual Claude Code usage)

1. Clone this repo and configure Claude Code per [INSTALLATION.md](INSTALLATION.md)
2. Start using `@agentname` prefix in your prompts
3. Use `@killua` for complex multi-step projects
4. Always end with `@higuruma` to audit before shipping

### From a single-agent setup

If you previously used a single custom agent file:

1. Add the 10 agent files to your agents directory
2. Your existing agent file continues to work unchanged
3. New agents are additive — no existing behavior changes

---

## Contributing

Agent definition changes follow this process:

1. Edit the agent `.md` file on a feature branch
2. Add test cases to `tests/VALIDATION_CHECKLIST.md`
3. Run the validation checklist against the changed agent
4. Get higuruma sign-off on the changes
5. Update this CHANGELOG with the version bump and changes
6. Merge to main
