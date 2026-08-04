---
name: writing-concision-review
description: Use this skill when tightening the prose of an English-language paper, technical document, or design doc that reads as roundabout, padded, or over-hedged. It works paragraph by paragraph to remove meta-sentences, paraphrase loops, empty abstractions, stacked hedges, and needless nominalization, and reports the net word reduction.
version: 1.0.0
---

# Writing Concision Review Skill

## Overview

This is phase 4 of a five-phase review of English technical writing. It removes words that carry no information. AI-generated technical prose is characteristically verbose in specific, recognizable ways, and this phase targets those patterns rather than length in general.

**When this skill applies:**
- Tightening a draft whose structure, flow, and claims are settled
- Reviewing text that reads as roundabout or evasive
- Cutting a document to a length limit

**Phase order:** structure → flow → evidence → concision (this skill). Run `writing-revision-review` after the author responds.

This phase runs last of the four because its decisions depend on `writing-evidence-review`: which hedges the evidence requires, and which vague phrases have a specific value available to replace them. Run it before the evidence phase and CO-003 and CO-004 become guesswork.

**Scope:** English-language documents. This suite reviews structure, argument, evidence, and length. It does not check grammar, articles, tense agreement, punctuation, or spelling; use a grammar checker for those. If the document is not in English, stop and say so rather than reviewing it.

## Input Restriction

Work paragraph by paragraph, and stay at the sentence level.

- Do not propose moving or deleting whole sections or paragraphs. Those belong to `writing-structure-review` and `writing-flow-review`; record them as deferred notes.
- Do not change what the text claims. Cutting a hedge that carries real uncertainty is a content change, not a concision fix.
- Rewrite in the document's existing register. Do not convert formal academic prose to a casual one.
- Deferrals to an earlier phase go under `Deferred to other phases`. Re-run that phase only when the note would change the outline; otherwise carry it into the next revision round.

## Review Policy

1. Every finding is a rewrite, not a comment. Show the replacement text.
2. Preserve meaning exactly. If a cut removes a qualification the evidence requires, do not make it. When `writing-evidence-review` has run, treat the hedges and scope statements it required as fixed text.
3. Do not add. If a rewrite is longer than the original, justify it or drop it.
4. Report the net word change (CO-007). A concision review with no reduction has failed.

## How to Use

1. Read the paragraph in full before rewriting anything.
2. Select the relevant checks from `checks/` instead of loading every check file by default. The Review Discipline check (CO-007) always applies.
3. Produce the rewritten paragraph, then the itemized findings.
4. Count words with a tool, not by eye: write the original and the rewrite to files and run `wc -w`. Count prose only, and exclude headings, code blocks, tables, figure captions, and reference lists. Apply the same exclusions to both sides.

## Output Format

Use this exact structure:

```markdown
Paragraph: <section> P<n>

Rewritten:
<the tightened paragraph>

Cuts:
- [CO-xxx] "<original>" -> "<replacement or (deleted)>", reason

Preserved deliberately:
- "<text>" - why this hedge or repetition must stay

Deferred to other phases:
- issue, target phase

Metrics:
- before: N / after: N / reduction: N (M%) words
```

Keep every heading even when there are no findings.

## Current Checks

| ID | Check | Category |
|----|-------|----------|
| CO-001 | Meta-sentences and preamble | Padding |
| CO-002 | Paraphrase loops | Redundancy |
| CO-003 | Empty abstractions | Specificity |
| CO-004 | Stacked hedging | Hedging |
| CO-005 | One idea per sentence | Sentence Structure |
| CO-006 | Nominalization and needless passive | Sentence Structure |
| CO-007 | Mandatory reduction reporting | Review Discipline |

## Check Files

All concision review checks are stored in:
- `checks/CO-001-meta-sentences.md`
- `checks/CO-002-paraphrase-loops.md`
- `checks/CO-003-empty-abstractions.md`
- `checks/CO-004-stacked-hedging.md`
- `checks/CO-005-one-idea-per-sentence.md`
- `checks/CO-006-nominalization-and-passive.md`
- `checks/CO-007-mandatory-reduction-reporting.md`
