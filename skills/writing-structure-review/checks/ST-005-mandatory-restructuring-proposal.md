# ST-005: Mandatory Restructuring Proposal

## Category
Review Discipline

## Description
A structure review must produce at least one concrete restructuring proposal: move, merge, delete, or reorder. Concluding "the structure is fine" is allowed only with an explicit justification.

## Why It Matters
- Reviewers default to sentence-level comments because they are cheaper to produce
- Without a forced proposal, a review of a badly ordered document returns only wording notes
- A restructuring proposal often removes the need for several sentence-level fixes

## Correct Approach
- Propose the change as an operation on the outline, naming source and destination
- If no change is warranted, write one line per section stating its contribution, and state that no two sections overlap and no dependency is inverted
- Never satisfy this check with a vague suggestion such as "consider reorganizing Section 4"

## Examples

### Weak
```text
The overall structure is reasonable. Consider tightening Section 4 and fixing terminology in Section 6.
```

### Strong
```text
Merge Section 4 (Implementation Notes) into Section 3 (Architecture); both describe the same component and Section 4 adds only two paragraphs.
Move Section 6.2 (Threat Model) before Section 5, which already assumes it.
Delete Section 7 (Future Work); it repeats the limitations in Section 6.3.
```

### Strong (no change warranted)
```text
No restructuring proposed.
2 Background - establishes the failure mode the method targets
3 Method - the contribution
4 Evaluation - tests the claim in Section 3
5 Limitations - bounds the claim
No two sections overlap; every term is defined before use.
```

## Review Guidance
One well-argued proposal beats five speculative ones. Do not manufacture changes to satisfy the check when the justified-no-change form applies.
