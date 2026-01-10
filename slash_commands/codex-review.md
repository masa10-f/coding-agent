---
description: Run Codex CLI review on current changes, then apply fixes and validate.
argument-hint: [--uncommitted | --base <branch> | --commit <sha>] [optional extra review instructions]
allowed-tools: >
  Bash(git status --porcelain*),
  Bash(git status *),
  Bash(git status),
  Bash(git diff --name-status*),
  Bash(git diff *),
  Bash(git diff),
  Bash(git branch --show-current*),
  Bash(git branch *),
  Bash(git branch),
  Bash(git ls-files --others*),
  Bash(git ls-files *),
  Bash(git ls-files),
  Bash(codex review *),
  Bash(codex review),
  Bash(npm *), Bash(pnpm *), Bash(yarn *), Bash(bun *),
  Bash(uv *), Bash(pytest *), Bash(ruff *), Bash(mypy *),
  Bash(make *), Bash(task *), Bash(just *), Bash(cargo *), Bash(go *), Bash(dotnet *), Bash(mvn *), Bash(gradle *)
---

# Codex review → apply fixes

## Task (follow strictly)
1) First, gather context by running:
   - `git branch --show-current` (current branch)
   - `git status --porcelain=v1` (status)
   - `git diff --name-status` (changed files)
   - `git ls-files --others --exclude-standard` (untracked files)
2) Run `codex review $ARGUMENTS -c hide_agent_reasoning=true` to get the review output.
3) Read the Codex review output and extract actionable issues, grouping by severity (P0/P1/P2) and scope.
4) Apply the minimum code changes needed to address them. Do not do refactors unless required to fix an issue.
5) Run the project's standard lint/test commands (prefer the lightest "quick" set first). If unsure, infer from package scripts / Makefile / task runner config.
6) If lint/tests fail, iterate until they pass.
7) Summarize what you changed and list any remaining review items you intentionally deferred (with rationale).
