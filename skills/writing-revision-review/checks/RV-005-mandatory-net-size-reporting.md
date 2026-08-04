# RV-005: Mandatory Net Size Reporting

## Category
Review Discipline

## Description
Report the document size before and after the revision as a number. Growth must be justified explicitly.

## Why It Matters
- Revision rounds grow documents monotonically unless the growth is measured
- A round that adds text everywhere and removes nothing has usually avoided every real fix
- The number is the cheapest available signal that a revision was additive rather than corrective

## Correct Approach
- Count words with `wc -w`, not by eye; an estimated count defeats the purpose of the check
- Count prose only. Exclude headings, code blocks, tables, figure captions, and reference lists, and apply the same exclusions to every round so the trend stays comparable
- Report before, after, and the signed net change, per revision round
- If the net change is positive, name what was added and why no deletion or restructuring could have answered the comments instead
- Track the trend across rounds; three consecutive additive rounds is itself a finding

## Examples

### Weak
```text
Addressed all review comments. The document is now clearer.
```

### Strong
```text
Metrics:
- before: 4,820 / after: 4,610 / net change: -210 words
- comments resolved: 6 / partial: 1 / substituted: 0 / unaddressed: 0

Two comments were answered by deleting the ambiguous passage rather than
clarifying it.
```

### Strong (justified growth)
```text
Metrics:
- before: 4,820 / after: 5,140 / net change: +320 words

Growth is the new derivation in Section 3.2, which three comments asked for. No
other section grew; Section 5 shrank by 90 words.
```

## Review Guidance
Growth is not a defect by itself. Missing evidence and missing derivations legitimately require text. The defect is unexplained growth, or growth spread evenly across sections nobody commented on.
