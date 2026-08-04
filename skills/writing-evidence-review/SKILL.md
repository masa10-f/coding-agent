---
name: writing-evidence-review
description: Use this skill when checking whether the claims in an English-language paper, technical report, or design doc are actually supported. It verifies that assertions have evidence, that claim strength matches that evidence, that terminology and numeric conditions are stated, and that figures and citations match the body text.
version: 1.0.0
---

# Writing Evidence Review Skill

## Overview

This is phase 3 of a five-phase review of English technical writing. It checks the relationship between what the document asserts and what it shows. Generated technical prose reliably produces confident, well-formed claims whose support is absent, weaker than stated, or located somewhere the text does not point to.

**When this skill applies:**
- Reviewing a paper's results, discussion, or abstract
- Reviewing a technical report or benchmark writeup
- Reviewing a design doc that justifies a decision with data

**Phase order:** structure → flow → evidence (this skill) → concision. Run `writing-revision-review` after the author responds.

This phase runs before `writing-concision-review` because concision decisions depend on its output: which hedges the evidence requires, and which vague phrases have a specific value to replace them with.

**Scope:** English-language documents. This suite reviews structure, argument, evidence, and length. It does not check grammar, articles, tense agreement, punctuation, or spelling; use a grammar checker for those. If the document is not in English, stop and say so rather than reviewing it.

## Input Restriction

Review one section at a time, with its figures, tables, and reference list available.

- Verify against the document's own evidence. Do not accept a claim because it is plausible or because you know it to be true elsewhere.
- Do not report wording or structure issues here; record them as deferred notes.
- When a claim's support is supposedly in another section, follow the pointer and check it. An unverifiable pointer is a finding.
- Deferrals to an earlier phase go under `Deferred to other phases`. Re-run that phase only when the note would change the outline; otherwise carry it into the next revision round.

## Review Policy

1. For each claim, name the specific evidence and its location, or record that there is none.
2. Distinguish three outcomes: supported, over-stated, unsupported. Do not merge the last two.
3. Prefer weakening a claim to adding new evidence, and prefer both to adding a hedge.
4. Report claims that are stronger than the evidence even when they are probably true.
5. State the corrected claim at whatever length accuracy requires. `writing-concision-review` tightens it afterward; do not trade accuracy for brevity here.

## How to Use

1. List the section's assertions, including those in figure captions and the abstract.
2. For each, locate its support: a number, a figure, a cited work, or a derivation.
3. Select the relevant checks from `checks/` instead of loading every check file by default.
4. Report unsupported claims first; they are the only findings that can invalidate the document.

## Output Format

Use this exact structure:

```markdown
Section: <heading>

Summary: Supported / Over-stated / Unsupported claims present

Unsupported claims:
- [location] claim, what evidence is missing, proposed fix (weaken / cite / measure / delete)

Over-stated claims:
- [location] claim, what the evidence actually supports, proposed wording

Terminology and units:
- [location] issue, proposed fix

Figures, tables, citations:
- [location] mismatch between the artifact and the body text, proposed fix

Deferred to other phases:
- [location] issue, target phase

Metrics:
- claims checked: N / unsupported: N / over-stated: N
```

Keep every heading even when there are no findings.

## Current Checks

| ID | Check | Category |
|----|-------|----------|
| EV-001 | Every claim names its evidence | Support |
| EV-002 | Claim strength matches the evidence | Calibration |
| EV-003 | Terminology consistency | Terminology |
| EV-004 | Numbers carry their conditions | Measurement |
| EV-005 | Figures and tables complement the text | Artifacts |
| EV-006 | Citations support what they are cited for | Citation |

## Check Files

All evidence review checks are stored in:
- `checks/EV-001-claim-names-its-evidence.md`
- `checks/EV-002-claim-strength-matches-evidence.md`
- `checks/EV-003-terminology-consistency.md`
- `checks/EV-004-numbers-carry-conditions.md`
- `checks/EV-005-figures-complement-text.md`
- `checks/EV-006-citations-support-claims.md`
