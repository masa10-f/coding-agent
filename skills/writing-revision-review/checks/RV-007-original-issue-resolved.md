# RV-007: The Original Issue Is Actually Resolved

## Category
Resolution

## Description
Check each change against the comment that prompted it. A change that addresses something adjacent to the comment is a substitution, not a resolution.

## Why It Matters
- Hard comments get answered with an easier nearby fix that looks responsive
- The reviewer sees activity at the flagged location and assumes the issue is closed
- Unresolved comments resurface a round later, having cost a full revision cycle

## Correct Approach
- Restate what the comment asked for before looking at the change
- Classify: resolved, partial, substituted, over-applied, unaddressed
- Name substitutions explicitly: what was asked, what was done instead
- A comment answered with "clarified the wording" when it asked for evidence is a substitution

## Examples

### Weak
```text
Comment: "What is the baseline for this 40% number?"
Revision: rewrote the sentence more clearly, still without naming the baseline.
Reported as: resolved.
```

### Strong
```text
Comment: "What is the baseline for this 40% number?"
Status: substituted. The sentence was rewritten but the baseline is still not
named. Required: state the comparison point and the absolute values.
```

## Review Guidance
Report unresolved comments plainly and without hedging. A comment the author deliberately declined is legitimate; record it as declined with the author's reason rather than as resolved.
