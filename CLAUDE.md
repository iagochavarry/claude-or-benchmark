# Claude-or-Benchmark

This project benchmarks different Claude model variations by:
1. Generating full-stack applications from a prompt template
2. Judging the output with a scoring agent

## Structure

```
app/
  {APP_NAME}/
    {VARIATION_NAME}/
      prompt-template.md   # filled-in prompt for this run
      solution/             # generated implementation
```

- `app/APP_NAME/VARIATION_NAME/` — One directory per app + model/harness combination.
- `prompt-template.md` (root) — Base template. Copy into each variation directory and fill in.
- `.claude/commands/judge.md` — Judge agent. Invoke with `/project:judge` in Claude Code.

### Naming Convention

- **APP_NAME**: the application domain (e.g. `social_media`, `task_manager`)
- **VARIATION_NAME**: the model or harness that generated it (e.g. `claude_code_sonnet`, `claude_code_opus`, `claude_code_or_kimi`)

## Workflow

1. Create `app/{APP_NAME}/{VARIATION_NAME}/`.
2. Copy `prompt-template.md` into that directory and fill in Stack/Application sections.
3. Feed the prompt to the model variation being tested.
4. Place the generated code in `solution/` within that directory.
5. Run `/project:judge` to score the implementation.
