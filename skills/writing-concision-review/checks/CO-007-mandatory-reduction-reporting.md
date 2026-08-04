# CO-007: Mandatory Reduction Reporting

## Category
Review Discipline

## Description
Report the size before and after in numbers. Additions are not part of this phase; if a rewrite is longer than the original, justify it or drop it.

## Why It Matters
- Without a number, a review can call itself a tightening pass while leaving the text the same length or longer
- Rewrites that improve clarity by adding words belong to a different phase and hide the absence of any cut
- The number makes the outcome auditable against the goal

## Correct Approach
- Count words with `wc -w`, not by eye; an estimated count defeats the purpose of the check
- Count prose only. Exclude headings, code blocks, tables, figure captions, and reference lists, and apply the same exclusions to both sides
- Report before, after, absolute reduction, and percentage
- List any rewrite that increased length under "Preserved deliberately" with its reason
- If the total reduction is zero, say so plainly and state why the text was already tight, per paragraph

## Examples

### Weak
```text
Tightened the paragraph and improved clarity throughout.
```

### Strong
```text
Metrics:
- before: 214 / after: 139 / reduction: 75 (35%) words

Preserved deliberately:
- "may not be reliable" - the single-seed caveat is required by the evidence
```

### Strong (no reduction available)
```text
Metrics:
- before: 190 / after: 190 / reduction: 0 (0%) words

No cuts available. P1 is three sentences, each carrying one measurement; P2 is the
single-sentence conclusion. No meta-sentences, paraphrase, or stacked hedges.
```

## Review Guidance
Do not hit a reduction target by deleting qualifications the evidence requires. A smaller reduction with meaning preserved is the correct outcome; record what you chose not to cut.
