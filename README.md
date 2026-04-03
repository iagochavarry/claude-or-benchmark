# Claude-or-Benchmark

Benchmark different AI model variations by generating full-stack applications from a standardized prompt and scoring the results.

## How It Works

1. **Prompt** — A stack-agnostic template (`prompt-template.md`) defines the app to build, with swappable Stack / Application / Requirements sections.
2. **Generate** — Feed the prompt to different model variations and collect their output.
3. **Judge** — A scoring agent (`.claude/commands/judge.md`) reviews each implementation against the prompt, scoring Frontend / Backend / Database from 1 to 5.

## Branching Strategy

Each application variation lives on its own branch:

```
app/<application_name>
```

Examples: `app/task-manager`, `app/ecommerce`, `app/blog-platform`

## Solution Naming

Inside `solution/`, each agent's output goes in a subfolder named after the agent that generated it:

```
solution/<AGENT_NAME>/
```

| Folder | Meaning |
|---|---|
| `solution/cc_sonnet/` | Claude Code with Sonnet |
| `solution/cc_opus/` | Claude Code with Opus |
| `solution/cc_or_kimi/` | Claude Code via OpenRouter with Kimi |

Convention: `cc_<model>` for Claude Code direct, `cc_or_<model>` for Claude Code via OpenRouter.

## Quick Start

```bash
# 1. Create a branch for your application
git checkout -b app/task-manager

# 2. Fill in prompt-template.md with your stack and app details

# 3. Generate the implementation with your chosen agent

# 4. Place output in solution/<AGENT_NAME>/

# 5. Score it (in Claude Code)
/project:judge
```

## Scoring Rubric

| Score | Meaning |
|---|---|
| 1 | Non-functional or missing |
| 2 | Minimal / broken |
| 3 | Functional but messy |
| 4 | Good |
| 5 | Excellent — production-ready |

Each dimension (Frontend, Backend, Database) is scored independently. See `.claude/commands/judge.md` for full rubric details.
