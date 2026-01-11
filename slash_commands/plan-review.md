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
   - `ls -lt ~/.claude/plans/*.md | head -1` (latest plan file)
   - Read the plan file content
2) Run `codex review $ARGUMENTS -c hide_agent_reasoning=true` with the plan file to get review feedback.
3) Read the Codex review output and extract actionable feedback:
   - Missing considerations
   - Potential risks or edge cases
   - Implementation order improvements
   - Unclear or ambiguous parts
4) Update the plan file based on the feedback. Do not rewrite entirely; apply targeted improvements.
5) Summarize what you changed and list any review items you intentionally deferred (with rationale).
