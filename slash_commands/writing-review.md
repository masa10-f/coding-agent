---
description: Run the writing-* review phases over an English document in order, then re-check the revision.
argument-hint: <path to document> [--phases 1-4 | --phase N | --revision] [optional scope notes]
allowed-tools: >
  Read, Grep, Glob, Edit, Write,
  Bash(wc *), Bash(wc),
  Bash(git diff *), Bash(git diff),
  Bash(git status --porcelain*), Bash(git status)
---

# Writing review pipeline

Drives the five `writing-*` skills in their required order. Each phase deliberately restricts what it looks at; running them together, or out of order, is what this command exists to prevent.

## Scope

English-language papers, technical reports, design docs, and long READMEs. The phases cover structure, argument, evidence, and length. They do **not** check grammar, articles, tense agreement, punctuation, or spelling. If the document is not in English, stop and say so.

## Task (follow strictly)

1) Read the target document from `$ARGUMENTS`. If no path is given, ask for one before doing anything else.

2) Run the phases in this order, one at a time. Do not start a phase before the previous one has produced its report.

   | Phase | Skill | Unit of review |
   |-------|-------|----------------|
   | 1 | `writing-structure-review` | headings only |
   | 2 | `writing-flow-review` | one section, paragraph level |
   | 3 | `writing-evidence-review` | one section, claim level |
   | 4 | `writing-concision-review` | one paragraph, sentence level |

   Evidence precedes concision because CO-003 and CO-004 depend on its output: which hedges the evidence requires, and which vague phrases have a specific value available to replace them.

3) After each phase, emit that skill's own Output Format verbatim. Do not merge phase reports into a single list; the per-phase headings and metrics are what make the review auditable.

4) Collect every `Deferred to other phases` entry as you go. After phase 4, re-run an earlier phase only if a deferred note would change the outline. Otherwise carry the notes into the next round and say so.

5) If `--revision` is passed, or the author has already responded to a previous round, run `writing-revision-review` instead of phases 1-4. It needs the original comments, the diff, and the full sections containing each change.

6) Count words with `wc -w` where a phase requires metrics (CO-007, RV-005). Do not estimate. Exclude headings, code blocks, tables, figure captions, and reference lists, and apply the same exclusions to both sides.

7) Report at the end: the phases run, the number of findings per phase, the net word change, and the deferred notes that remain open.

## Arguments

- `--phase N` runs only phase N. Say in the report which earlier phases were skipped and what that makes unreliable.
- `--phases 1-4` is the default.
- `--revision` runs phase 5 only.
- Any remaining text is treated as scope notes, for example a venue's section-order constraint or a length limit.
