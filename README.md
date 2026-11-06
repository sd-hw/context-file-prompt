# The context file prompt

A free prompt from [@sd_hw.cv](https://instagram.com/sd_hw.cv) that writes a small, specific context file
(`CLAUDE.md`, `AGENTS.md` or Cursor rules) your coding agent will actually follow.

**Use it:** open [`context-file-prompt.md`](context-file-prompt.md), copy everything below the line, and paste it into
Claude Code, Cursor, Codex or any agent that can read your repo. It reads the repo first, asks you up to 8 questions,
drafts the file, audits it, and tells you how to test it.

## The 3 rules it follows

1. **Skip the obvious.** Only write what the agent can't work out from the code: exact commands, gotchas,
   decisions, things it got wrong twice. No repo tours.
2. **Be specific.** "Run `npm test` before committing", not "test your changes".
3. **Keep it short.** Under 200 lines (Anthropic's target for CLAUDE.md). Longer files get followed less.

## Why (the receipts)

- Gloaguen et al., *Evaluating AGENTS.md: Are Repository-Level Context Files Helpful for Coding Agents?*, ETH Zurich and
  LogicStar.ai, [arXiv 2602.11988](https://arxiv.org/abs/2602.11988) (2026 preprint). Across 4 agent setups and 438 tasks
  on Python repos, auto-generated context files didn't improve success (it dropped in 5 of 8 settings) and raised cost
  by over 20% on average. Repository overviews weren't helpful. Specific instructions were followed. Their advice:
  omit auto-generated files for now, and keep human-written ones to what isn't already in the codebase.
- Anthropic, [Claude Code memory](https://code.claude.com/docs/en/memory) and
  [best practices](https://code.claude.com/docs/en/best-practices): target under 200 lines; be specific; CLAUDE.md is
  context, not enforced configuration (use hooks for hard rules).
- Cursor, [Rules](https://cursor.com/docs/context/rules): keep rules under 500 lines, avoid vague guidance, add rules only
  for repeated mistakes.
- [agents.md](https://agents.md): AGENTS.md as "a README for agents".

## Honest note

The study tested agents' own default auto-generated files. This prompt is built around its findings, but it hasn't been
benchmarked. That's why it ends with a with-vs-without test: keep the file only if it helps on your repo.

Not affiliated with Anthropic, Cursor, OpenAI, ETH Zurich or LogicStar.ai.

License: MIT.
