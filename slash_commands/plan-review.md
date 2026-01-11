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
2) Run `codex review "$PLAN_FILE" $ARGUMENTS -c hide_agent_reasoning=true` to get review feedback on the plan file.
3) Read the Codex review output and extract actionable feedback:
   - Missing considerations
   - Potential risks or edge cases
   - Implementation order improvements
   - Unclear or ambiguous parts
4) Update the plan file based on the feedback. Do not rewrite entirely; apply targeted improvements.
5) Summarize what you changed and list any review items you intentionally deferred (with rationale).
