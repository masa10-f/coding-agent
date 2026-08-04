---
name: writing-revision-review
description: Use this skill after an author or agent has revised an English-language document in response to review comments, to check whether the revision actually fixed the issue without damaging the surrounding text. It detects defensive additions, fixes applied to only one of several affected places, mechanical over-application, and append-only revision that ignores restructuring.
version: 1.0.0
---

# Writing Revision Review Skill

## Overview

This is phase 5 of a five-phase review of English technical writing, and the one that catches the failure modes specific to agent-written revisions. An agent asked to fix a comment tends to fix exactly the flagged location, add defensive qualifications around it, and leave the surrounding text inconsistent, while the document only ever grows.

**When this skill applies:**
- After a revision responding to review comments from any of the earlier phases
- After an agent has been asked to "fix" a document
- Reviewing a document across several revision rounds

**Phase order:** structure → flow → evidence → concision, then this skill after each round of responses.

**Scope:** English-language documents. This suite reviews structure, argument, evidence, and length. It does not check grammar, articles, tense agreement, punctuation, or spelling; use a grammar checker for those. If the document is not in English, stop and say so rather than reviewing it.

## Input Restriction

Never review the changed sentence in isolation.

For each change, read:
1. The original review comment.
2. The diff.
3. The entire section containing the change.
4. The headings of the preceding and following sections.

A revision that is locally correct and globally wrong is the specific defect this phase exists to find, and it is invisible from the diff alone.

## Review Policy

1. Judge each change on two axes: did it resolve the comment, and what did it cost elsewhere.
2. Treat growth as a signal. A revision that only adds has almost certainly avoided the real fix.
3. A fix applied in one place must be checked against every other place the same issue occurs.
4. Report both under- and over-application. Mechanical propagation is a defect, not thoroughness.
5. Report the net size change in numbers (RV-005).

## How to Use

1. Pair each review comment with the change or changes that responded to it.
2. Classify each pair: resolved, partial, substituted, over-applied, unaddressed.
3. Select the relevant checks from `checks/` instead of loading every check file by default. The Review Discipline check (RV-005) always applies.
4. Report ripple damage before residual comment-level issues; a broken section costs more than an unfixed comment.
5. Count words with a tool, not by eye: run `wc -w` on the before and after revisions. Count prose only, and exclude headings, code blocks, tables, figure captions, and reference lists. Apply the same exclusions to both sides and to every round.

## Output Format

Use this exact structure:

```markdown
Summary: Clean / Needs rework / Regressed

Per comment:
- [comment] -> resolved | partial | substituted | over-applied | unaddressed
  what changed, and whether it answers the comment

Ripple damage:
- [location] what the change broke in the surrounding text, proposed fix

Defensive additions:
- [location] the qualification or note added instead of a fix, proposed replacement

Restructuring not considered:
- [comment] the move / merge / delete that would have solved it without adding text

Metrics:
- before: N / after: N / net change: +N or -N words
- comments resolved: N / partial: N / substituted: N / unaddressed: N
```

Keep every heading even when there are no findings. If the net change is positive, the review must state why the document had to grow.

## Current Checks

| ID | Check | Category |
|----|-------|----------|
| RV-001 | Ripple check on the surrounding text | Consistency |
| RV-002 | Defensive additions | Revision Behavior |
| RV-003 | Under-application to sibling occurrences | Coverage |
| RV-004 | Mechanical over-application | Coverage |
| RV-005 | Mandatory net size reporting | Review Discipline |
| RV-006 | Restructuring considered before appending | Revision Behavior |
| RV-007 | The original issue is actually resolved | Resolution |

## Check Files

All revision review checks are stored in:
- `checks/RV-001-ripple-check.md`
- `checks/RV-002-defensive-additions.md`
- `checks/RV-003-under-application.md`
- `checks/RV-004-mechanical-over-application.md`
- `checks/RV-005-mandatory-net-size-reporting.md`
- `checks/RV-006-restructuring-before-appending.md`
- `checks/RV-007-original-issue-resolved.md`
