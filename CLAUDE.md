# Claude-or-Benchmark

This project benchmarks different Claude model variations by:
1. Generating full-stack applications from a prompt template
2. Judging the output with a scoring agent

## Structure

- `prompt-template.md` — Stack-agnostic bootstrap prompt. Fill in the Stack/Application/Requirements sections per run.
- `.claude/commands/judge.md` — Judge agent prompt. Invoke with `/project:judge` in Claude Code.
- `app/` — Generated implementations, organized by app and variation.

### App Directory Convention

```
app/<APP_NAME>/<VARIATION_NAME>/
```

- `APP_NAME` — the application domain (e.g. `social_media`, `task_manager`, `ecommerce`)
- `VARIATION_NAME` — the model/harness that generated it (e.g. `claude_code_sonnet`, `claude_code_opus`, `claude_code_or_kimi`)

Example:
```
app/social_media/claude_code_sonnet/
app/social_media/claude_code_opus/
app/social_media/claude_code_or_sonnet/
app/social_media/claude_code_or_kimi/
```

## Workflow

1. Fill in `prompt-template.md` sections for your target stack and app.
2. Feed the prompt to the model variation being tested.
3. Place the generated code in `app/<APP_NAME>/<VARIATION_NAME>/`.
4. Run `/project:judge` and specify which variation to review.
