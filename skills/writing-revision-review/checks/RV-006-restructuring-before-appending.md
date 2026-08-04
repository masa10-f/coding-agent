# RV-006: Restructuring Considered Before Appending

## Category
Revision Behavior

## Description
For each comment answered by adding text, state whether moving, merging, or deleting existing text would have answered it instead, and why that option was rejected.

## Why It Matters
- Appending is the cheapest response to a comment and is almost always the first one reached for
- Many comments are symptoms of a structural problem; adding text at the symptom leaves the cause and adds length
- Requiring the alternative to be stated is what forces it to be considered at all

## Correct Approach
- For every addition, name the move, merge, or deletion that was the alternative
- Reject the alternative with a reason, not by omission
- Comments phrased as "unclear", "why is this here", "this repeats Section N", or "out of order" are structural until shown otherwise
- When the alternative is better, propose it and revert the addition

## Examples

### Weak
```text
Comment: "It is unclear how this relates to Section 2."
Revision: added a paragraph at the start of Section 5 explaining the relationship.
```

### Strong
```text
Comment: "It is unclear how this relates to Section 2."
Alternative considered: move Section 5.1 directly after Section 2, which is what
it elaborates. Chosen: the move. Net -80 words, and the new transition paragraph
was not needed.
```

### Strong (addition justified)
```text
Comment: "The derivation of Eq. 4 is missing."
Alternative considered: cite [9] instead of deriving it. Rejected: [9] derives a
different variant, and the difference is the contribution. Added 140 words.
```

## Review Guidance
Some comments genuinely ask for content that does not exist, and adding it is correct. The requirement is that the alternative be named and rejected on the record, not that additions be avoided.
