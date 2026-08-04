---
name: writing-flow-review
description: Use this skill when reviewing how paragraphs connect within a section of an English-language paper, technical document, or design doc, after the overall structure has been reviewed. It checks claim placement, connective accuracy, paragraph handoff, single-topic paragraphs, and bullet lists used to avoid writing an argument.
version: 1.0.0
---

# Writing Flow Review Skill

## Overview

This is phase 2 of a five-phase review of English technical writing. It works one section at a time and evaluates whether paragraphs form an argument or merely sit next to each other. AI-generated prose frequently produces locally correct paragraphs whose connective tissue is missing or false.

**When this skill applies:**
- Reviewing the body of a section after `writing-structure-review`
- Reviewing a section that reads as a list of facts rather than an argument
- Reviewing a section that grew by insertion

**Phase order:** structure → flow (this skill) → evidence → concision. Run `writing-revision-review` after the author responds.

**Scope:** English-language documents. This suite reviews structure, argument, evidence, and length. It does not check grammar, articles, tense agreement, punctuation, or spelling; use a grammar checker for those. If the document is not in English, stop and say so rather than reviewing it.

## Input Restriction

Review one section at a time, and stay inside it.

- Do not propose moving content between sections. That belongs to `writing-structure-review`; if you find such a problem, record it as a deferred note and move on.
- Do not rewrite wording for brevity. That belongs to `writing-concision-review`.
- Read the whole section before reporting anything. Paragraph-by-paragraph reporting produces the same append-only bias this phase exists to catch.
- Deferrals to an earlier phase go under `Deferred to other phases`. Re-run that phase only when the note would change the outline; otherwise carry it into the next revision round.

## Review Policy

1. Report at the paragraph level: placement, order, connection, split, merge, deletion.
2. Every finding must name the two paragraphs whose relationship is broken, not just the offending sentence.
3. Prefer reordering and deleting paragraphs over inserting transitional ones.
4. Do not add a transition sentence to paper over a real ordering problem.

## How to Use

1. Number the paragraphs in the section.
2. Write the claim of each paragraph in one clause. A paragraph whose claim needs two clauses is an FL-004 candidate.
3. Read the claims in sequence and check whether they form an argument.
4. Select the relevant checks from `checks/` instead of loading every check file by default. The Review Discipline check (FL-006) always applies.

## Output Format

Use this exact structure:

```markdown
Section: <heading>

Summary: Coherent / Fixable / Broken

Paragraph claims:
P1: <one clause>
P2: <one clause>
...

Flow issues:
- [P<n> -> P<m>] what connection is broken, why it matters, proposed fix (reorder / split / merge / delete)

Removable paragraphs:
- [P<n>] why the argument survives without it, or "none found: <reason>"

Deferred to other phases:
- [P<n>] issue, target phase

Metrics:
- paragraphs reordered: N / split: N / merged: N / deleted: N / transitions added: N
```

Keep every heading even when a section has no findings. If `transitions added` exceeds `paragraphs deleted`, state why.

## Current Checks

| ID | Check | Category |
|----|-------|----------|
| FL-001 | Lead with the claim | Placement |
| FL-002 | Connective matches the actual logic | Logic |
| FL-003 | Paragraph handoff | Continuity |
| FL-004 | One topic per paragraph | Scope |
| FL-005 | Bullet lists used to avoid arguing | Argument |
| FL-006 | Mandatory removable-paragraph search | Review Discipline |

## Check Files

All flow review checks are stored in:
- `checks/FL-001-lead-with-the-claim.md`
- `checks/FL-002-connective-matches-logic.md`
- `checks/FL-003-paragraph-handoff.md`
- `checks/FL-004-one-topic-per-paragraph.md`
- `checks/FL-005-bullet-list-escape.md`
- `checks/FL-006-mandatory-removable-paragraph.md`
