# Claude-or-Benchmark

This project benchmarks different Claude model variations by:
1. Generating full-stack applications from a prompt template
2. Judging the output with a scoring agent

## Structure

- `prompt-template.md` — Stack-agnostic bootstrap prompt. Fill in the Stack/Application/Requirements sections per run.
- `.claude/commands/judge.md` — Judge agent prompt. Invoke with `/project:judge` in Claude Code.
- `solution/` — Place generated implementations here for judging.

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

Naming convention: `cc_<model>` for Claude Code, `cc_or_<model>` for Claude Code via OpenRouter.

Examples:
- `solution/cc_sonnet/` — Claude Code with Sonnet
- `solution/cc_opus/` — Claude Code with Opus
- `solution/cc_or_kimi/` — Claude Code via OpenRouter with Kimi

## Workflow

1. Create a branch: `git checkout -b app/<application_name>`
2. Fill in `prompt-template.md` sections for your target stack and app.
3. Feed the prompt to the model variation being tested.
4. Place the generated code in `solution/<AGENT_NAME>/`.
5. Run `/project:judge` to score the implementation.
