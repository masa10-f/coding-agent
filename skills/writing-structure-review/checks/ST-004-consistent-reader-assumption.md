# ST-004: Consistent Reader Assumption

## Category
Audience

## Description
The level of assumed background must stay consistent across sections.

## Why It Matters
- Mixed levels signal that sections were written or expanded at different times for different reasons
- Over-explaining basics next to under-explaining the contribution wastes the reader's attention where it matters least
- Inconsistent level is usually the visible symptom of an unresolved audience decision

## Correct Approach
- Name the target reader in one sentence, for example "an ML researcher who does not work on retrieval"
- Check each section against that reader: what is over-explained, what is skipped
- Cut the over-explained material rather than expanding the under-explained material, unless the under-explained part is the contribution
- Move genuinely necessary background for a non-target reader into an appendix

## Examples

### Weak
```text
2. Background - defines what a neural network is (three paragraphs)
5. Proposed Method - introduces the novel loss term in one sentence with no derivation
```

### Strong
```text
2. Background - states only the two properties of the base model the method relies on
5. Proposed Method - derives the novel loss term, with the intuition stated first
```

## Review Guidance
Tutorials and onboarding docs legitimately explain basics at length. Apply this check against the document's declared audience, not against an expert default.
