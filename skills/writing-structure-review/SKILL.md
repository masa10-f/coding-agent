---
name: writing-structure-review
description: Use this skill when reviewing the overall structure of an English-language paper, technical document, design doc, or README before reviewing its prose. It evaluates section ordering, section purpose, scattered explanations, and reader assumptions from the heading outline alone, and produces either a concrete restructuring proposal or an explicit justification for proposing none.
version: 1.0.0
---

# Writing Structure Review Skill

## Overview

This is phase 1 of a five-phase review of English technical writing. It evaluates whether the document's skeleton supports its claim. AI-generated documents tend to grow by appending sections rather than reorganizing them, so this phase exists to force a restructuring decision before any sentence-level work begins.

**When this skill applies:**
- Reviewing a paper, technical report, design doc, or long README
- Reviewing an outline before the body is written
- Reviewing a document that grew through repeated additions

**Phase order:** structure (this skill) → flow → evidence → concision. Run `writing-revision-review` after the author responds to any of these.

**Scope:** English-language documents. This suite reviews structure, argument, evidence, and length. It does not check grammar, articles, tense agreement, punctuation, or spelling; use a grammar checker for those. If the document is not in English, stop and say so rather than reviewing it.

## Input Restriction

Do not read the body text in this phase.

1. Extract the heading tree.
2. Write a one-line summary of each section, derived from its heading and, at most, its first and last sentence.
3. Review using only that outline.

This restriction is the point of the phase. Reading full paragraphs pulls the review toward wording issues and the structural problem goes unreported.

Two checks need more than the outline. For ST-002 and ST-003, you may search the body for where a specific term or concept occurs, and read only enough around each hit to confirm whether it is a definition or a use. Search for occurrences; do not read the sections through.

If a section cannot be summarized in one line from its heading and boundary sentences, record that as an ST-001 finding rather than reading further.

## Review Policy

1. Judge every section against the document's single main claim.
2. Prefer moving, merging, and deleting over adding.
3. Do not report wording, grammar, or terminology issues here. Defer them to later phases.
4. A review that proposes no structural change must justify that conclusion explicitly (ST-005, ST-006).

## How to Use

1. Identify the document's main claim in one sentence. If you cannot, report that as the top finding and stop.
2. Build the outline as described in Input Restriction.
3. Select the checks in `checks/` that match the document type instead of loading every check file by default. The Review Discipline checks (ST-005, ST-006) always apply.
4. Produce a before/after outline, not a list of comments.

## Output Format

Use this exact structure:

```markdown
Main claim: <one sentence, or "not identifiable">

Summary: Sound / Fixable / Needs restructuring

Current outline:
1. <heading> - <one-line purpose>
...

Proposed outline:
1. <heading> - <change: keep / move from N / merge with N / delete / new>
...

Structural issues:
- [section] issue, why it weakens the claim, proposed fix

Merge or delete candidates:
- [section] reason, what is lost, where the content goes

Deferred to other phases:
- [section] issue, target phase

Metrics:
- sections moved: N / merged: N / deleted: N / added: N
```

Keep every heading even when a section has no findings. If `added` exceeds `deleted + merged`, state why the document must get longer.

## Current Checks

| ID | Check | Category |
|----|-------|----------|
| ST-001 | Every section earns its place | Purpose |
| ST-002 | Given-before-new ordering | Ordering |
| ST-003 | Scattered explanation of one concept | Cohesion |
| ST-004 | Consistent reader assumption | Audience |
| ST-005 | Mandatory restructuring proposal | Review Discipline |
| ST-006 | Mandatory merge or delete candidate | Review Discipline |

## Check Files

All structure review checks are stored in:
- `checks/ST-001-section-earns-its-place.md`
- `checks/ST-002-given-before-new.md`
- `checks/ST-003-scattered-explanation.md`
- `checks/ST-004-consistent-reader-assumption.md`
- `checks/ST-005-mandatory-restructuring-proposal.md`
- `checks/ST-006-mandatory-merge-or-delete.md`
