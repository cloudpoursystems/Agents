# Installation

Setup guide for deploying the claude-agents system in Claude Code.

---

## Prerequisites

- Claude Code CLI installed (`npm install -g @anthropic-ai/claude-code` or via the desktop app)
- Git
- A Claude account with API access

---

## Step 1: Clone the Repository

```bash
git clone https://github.com/cloudpoursystems/claude-agents.git
cd claude-agents
```

---

## Step 2: Configure Claude Code to Use the Agents

Claude Code loads custom agents from a designated directory. Point it at this repo.

### Option A: Global agents directory

Set the agents directory in your Claude Code global config (`~/.claude/settings.json`):

```json
{
  "agentsDirectory": "/path/to/claude-agents"
}
```

### Option B: Project-level agents

Copy or symlink the agent `.md` files into your project's `.claude/agents/` directory:

```bash
mkdir -p .claude/agents
cp /path/to/claude-agents/*.md .claude/agents/
```

Or symlink the whole directory:

```bash
ln -s /path/to/claude-agents .claude/agents
```

### Option C: CLAUDE.md reference

Add an agents section to your project's `CLAUDE.md`:

```markdown
## Agents

This project uses the claude-agents system. Agent files are in `.claude/agents/`.

Available agents: toji, hisoka, gon, yuji, higuruma, pain, sukuna, grimmjow, shanks, killua
```

---

## Step 3: Verify Installation

In a Claude Code session, test that agents are discoverable:

```
@toji What languages do you support?
```

Expected: toji responds with its capabilities.

```
@killua List the available agents on this team.
```

Expected: killua enumerates all 10 agents with their domains.

---

## Step 4: Configure Skills (Optional but Recommended)

Agents invoke skills via the `Skill` tool. Skills are separate from agents — they're reusable prompt modules registered in your Claude Code skill registry.

### Install skills referenced by agents

Each agent's skill table references skill identifiers. These must be registered in your skill registry for the `Skill` tool invocations to resolve.

Check your skill registry location:

```bash
ls ~/.claude/skills/
# or
ls .claude/skills/
```

Skills are `.md` files named to match the skill identifier. For example, `marketing-skills:paid-ads` corresponds to a file at `marketing-skills/paid-ads.md`.

If a skill isn't installed, the agent will proceed without it but may produce lower-quality output. The agent will log a warning when a skill invocation fails to resolve.

### Skill bundles by agent

| Agent | Skill bundle |
|-------|-------------|
| toji | `feature-dev`, `code-review`, `pr-review-toolkit`, `mcp-server-dev`, `superpowers` |
| hisoka | `figma`, `frontend-design`, `brand-guidelines`, `theme-factory` |
| gon | `deep-research`, `pm-market-research`, `marketing-skills` |
| yuji | `searchfit-seo`, `marketing-skills`, `elements-of-style` |
| higuruma | `pr-review-toolkit`, `code-review`, `superpowers` |
| pain | `devops-skills`, `superpowers` |
| sukuna | `pm-data-analytics`, `marketing-skills` |
| grimmjow | `marketing-skills`, `searchfit-seo`, `pm-go-to-market`, `pm-marketing-growth` |
| shanks | `pm-execution`, `pm-product-discovery`, `pm-product-strategy`, `pm-market-research`, `pm-go-to-market` |
| killua | `superpowers`, `great_cto` |

---

## Environment Variables

Some agents and skills require API keys for external services. Set these in your shell or `.env`:

```bash
# Required for web research (gon, grimmjow, shanks)
export ANTHROPIC_API_KEY=sk-ant-...

# Required for Figma integration (hisoka)
export FIGMA_ACCESS_TOKEN=figd_...

# Required for cloud infrastructure (pain)
export AWS_PROFILE=your-profile
export AWS_REGION=us-east-1

# Optional: LangSmith for LLM observability (toji, sukuna)
export LANGSMITH_API_KEY=ls__...
export LANGSMITH_PROJECT=your-project
```

---

## Updating Agents

Pull the latest agent definitions:

```bash
cd /path/to/claude-agents
git pull origin main
```

Agent files are hot-reloaded by Claude Code — no restart required.

---

## Troubleshooting

### Agent not found / not responding

1. Verify the agent `.md` file exists in the configured agents directory
2. Check the frontmatter `name` field matches what you're using (`@toji`, not `@Toji`)
3. Confirm the agents directory path in your Claude Code config

### Skill invocations failing silently

1. Check that skill files exist in your skills directory
2. Verify the skill identifier format matches: `bundle:skill-name` or `skill-name`
3. Enable skill debug logging in Claude Code settings

### Agent produces generic responses (not using skills)

The agent's system prompt instructs it to invoke the `Skill` tool before starting. If skills aren't resolving, the agent falls back to base knowledge. This is expected degradation, not a bug. Install the required skill bundles for full capability.

### Model availability

All agents use `claude-opus-4-7`. If this model is unavailable in your region or plan, update the `model:` field in each agent `.md` file to an available model:

```yaml
---
name: toji
model: claude-sonnet-4-6  # fallback if opus-4-7 unavailable
---
```

---

## Claude Code Configuration Reference

Full `settings.json` example with agents configured:

```json
{
  "agentsDirectory": "~/.claude/agents",
  "model": "claude-opus-4-7",
  "permissions": {
    "allow": [
      "Bash(git:*)",
      "Bash(npm:*)",
      "Bash(terraform:*)"
    ]
  }
}
```
