# FL-003: Paragraph Handoff

## Category
Continuity

## Description
Each paragraph should start from where the previous one left off. A paragraph that introduces an unrelated topic without a stated reason breaks the handoff.

## Why It Matters
- Broken handoffs make the reader reconstruct the argument themselves
- Inserted paragraphs sever the link between the paragraphs they were dropped between
- The fix is usually reordering, not adding a bridging sentence

## Correct Approach
- Read the paragraph claims in sequence and mark every point where the topic changes without warrant
- Reorder so that related paragraphs are adjacent
- If two paragraphs genuinely belong in sequence, make the dependency explicit in the second one's first sentence
- If a paragraph was inserted between two that used to connect, move it out rather than bridging around it

## Examples

### Weak
```text
P1: The index is rebuilt nightly.
P2: Query latency is dominated by disk seeks.
P3: The nightly rebuild is scheduled at 02:00 UTC to avoid peak traffic.
```
P2 severs P1 and P3.

### Strong
```text
P1: The index is rebuilt nightly, scheduled at 02:00 UTC to avoid peak traffic.
P2: Between rebuilds, query latency is dominated by disk seeks.
```

## Review Guidance
A deliberate topic shift at a subsection boundary is not a broken handoff. Apply this check within a run of paragraphs that share a subheading.
