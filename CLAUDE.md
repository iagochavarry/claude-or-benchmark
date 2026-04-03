# Claude-or-Benchmark

This project benchmarks different Claude model variations by:
1. Generating full-stack applications from a prompt template
2. Judging the output with a scoring agent

## Structure

- `prompt-template.md` — Stack-agnostic bootstrap prompt. Fill in the Stack/Application/Requirements sections per run.
- `.claude/commands/judge.md` — Judge agent prompt. Invoke with `/project:judge` in Claude Code.
- `solution/` — Place generated implementations here for judging.

## Workflow

1. Fill in `prompt-template.md` sections for your target stack and app.
2. Feed the prompt to the model variation being tested.
3. Place the generated code in `solution/`.
4. Run `/project:judge` to score the implementation.
