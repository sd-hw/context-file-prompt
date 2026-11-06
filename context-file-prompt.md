# The context file prompt

Paste everything below the line into Claude Code, Cursor, Codex or any coding agent that can read your repo.
It writes a `CLAUDE.md`, `AGENTS.md` or `.cursor/rules/project.mdc`, following the research and the official docs.

---

You are going to write a context file for this repository: the file a coding agent reads at the start of every session.

Target file: {{CLAUDE.md | AGENTS.md | .cursor/rules/project.mdc}}. If I didn't pick one, ask me which agent I use.

## Why this file must be small

- An ETH Zurich study (Gloaguen et al., arXiv 2602.11988, 2026) found that auto-generated context files
  didn't raise task success and raised agent cost by over 20% on average. Repository overviews didn't help.
  Agents DID follow specific instructions (a tool named in the file got used; unnamed, it almost never did).
- Anthropic's docs: the file works best when it "only holds what Claude couldn't work out from the code
  itself". Target under 200 lines; "longer files consume more context and reduce adherence".
- Cursor's docs: keep rules under 500 lines, avoid vague guidance, add rules only for mistakes the agent repeats.

So your job is NOT to describe the repo. It is to write down only what an agent would get wrong without being told.

## Step 1. Read before you write (don't write anything yet)

Read the README, the package manifest(s), lockfiles, CI workflows, Makefile or task runner, linter and
formatter configs, test setup, `.env.example`, and any existing CLAUDE.md, AGENTS.md or rules files.
Collect:
- the exact commands for install, dev server, build, test (whole suite and a single test), lint, typecheck, format,
- anything surprising: a non-default package manager, a custom test runner, generated code that must not be
  edited by hand, a monorepo layout, required env vars, slow or flaky tests.

If you can run commands, run the test, lint and typecheck commands to confirm they work. Never guess a command.
Mark anything you couldn't confirm as `(unverified)`.

## Step 2. Interview me (one message, numbered, max 8 questions)

Ask only what the code can't tell you, for example:
1. What has an AI agent got wrong in this repo more than once?
2. Which decisions aren't visible in the code (why this library, why not that pattern)?
3. Where is the code misleading (legacy folders, files that look used but aren't)?
4. What must an agent never do (touch migrations, edit generated files, push to main, change public APIs)?
5. Commit message and PR conventions?
6. Anything about running locally that isn't in the README?
Skip any question the repo already answers. Wait for my answers.

## Step 3. Draft with these rules

- **Only what the code can't show.** For every line ask: "Could the agent find this by reading the code?"
  and "Would it actually go and look?" If both are yes, cut it.
- **No repo tour.** No directory listing and no "this project is a…" overview, unless the repo has no README at all.
- **Specific, checkable lines.** "Run `npm test` before committing", not "test your changes".
  Exact commands in backticks, exact paths, exact names.
- **Short.** Under 200 lines; aim for 30–80. Bullets under a few headers:
  `## Commands`, `## Conventions`, `## Gotchas`, `## Decisions`, `## Never`.
- **Point, don't paste.** Reference files (`@docs/api.md` in CLAUDE.md, or a plain path) instead of copying
  their contents. Leave style rules a linter already enforces to the linter.
- **No contradictions.** If two rules conflict, ask me which one wins.
- **No secrets.** No keys, tokens or real `.env` values. Mention variable names only.
- **Hard rules aren't prose.** If something must never happen, don't shout IMPORTANT. Put it under `## Never`,
  then tell me which ones should become a hook, a deny rule or a CI check, because the file is context, not enforcement.

## Step 4. Audit your own draft

Before showing me, go through it line by line and:
1. Cut every line that fails the two questions in Step 3.
2. Rewrite every vague line into a command, path or example.
3. Check each command against what you confirmed in Step 1.
4. Count the lines. Over 200: cut or move topic-specific parts into scoped rules (`.claude/rules/` with `paths:`,
   Cursor "Apply to Specific Files" rules, or a nested AGENTS.md in that folder).

## Step 5. Give me

1. The file, ready to save.
2. A short list of what you left out and why (so I can disagree).
3. Rules from `## Never` that should become hooks, deny rules or CI checks.
4. A 2-minute test: one real task to run once with the file and once without, comparing whether it
   followed the commands, the number of steps and the result. Keep the file only if it helps.

Then stop. When the agent repeats a mistake later, add one line for it. Don't regenerate the whole file.
