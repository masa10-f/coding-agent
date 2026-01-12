---
description: Codex CLI で現在のプランをレビューし、フィードバックに基づいてプランを更新する
argument-hint: [追加のレビュー指示（オプション）]
allowed-tools: >
  Bash(ls *),
  Bash(cat *),
  Bash(codex review *),
  Bash(codex *),
  Read(*),
  Edit(*)
---

# Plan Review → プラン更新

## Task (follow strictly)
1) First, detect the latest plan file:
   - Run `ls -t ~/.claude/plans/*.md | head -1` to get the latest plan file path
   - Store the path (e.g., `PLAN_FILE=~/.claude/plans/example.md`)
   - Read the plan file content using the Read tool
2) Run Codex review in **quiet mode** (avoid tool/command logs in the transcript) and capture only the final review message:
   - `codex exec -o /tmp/plan-review.last.md review "$PLAN_FILE" $ARGUMENTS -c hide_agent_reasoning=true >/tmp/plan-review.run.log 2>&1`
   - Read `/tmp/plan-review.last.md` and use it as the review output.
   - If `/tmp/plan-review.last.md` is missing/empty, re-run without redirection to see the error output.
3) Read the Codex review output and extract actionable feedback:
   - Missing considerations
   - Potential risks or edge cases
   - Implementation order improvements
   - Unclear or ambiguous parts
4) Update the plan file based on the feedback. Do not rewrite entirely; apply targeted improvements.
5) Summarize what you changed and list any review items you intentionally deferred (with rationale).
