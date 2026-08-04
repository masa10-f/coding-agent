# RV-001: Ripple Check on the Surrounding Text

## Category
Consistency

## Description
Every change must be checked against the section around it for new duplication, contradiction, or broken connections.

## Why It Matters
- A revision that answers a comment perfectly can still leave the section incoherent
- Content added at the flagged location often duplicates something two paragraphs later
- The reader sees the section, not the diff, so local correctness is not enough

## Correct Approach
- Read the whole section after the change, not just the changed lines
- Check three things: does the new text repeat something already stated, contradict it, or break the handoff between its neighbors
- Check whether an earlier forward reference to this passage still holds
- Prefer resolving the duplication by deleting the older occurrence or the new one, not by rewording both

## Examples

### Weak
```text
Comment: "Section 3 never says why the cache is disabled by default."
Revision: added a paragraph at the end of Section 3 explaining the default.
Result: Section 3.4 already explained it, two paragraphs later, with a different reason.
```

### Strong
```text
Revision: moved the existing explanation from Section 3.4 to the point where the
default is first mentioned, and reconciled the two stated reasons; the correct one
is memory pressure, not startup latency.
```

## Review Guidance
Ripple damage outranks the original comment. If the change resolved the comment but broke the section, report it as needing rework, not as resolved with a note.
