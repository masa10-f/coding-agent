# FL-001: Lead With the Claim

## Category
Placement

## Description
A paragraph's claim belongs in its first sentence. Setup, caveats, and derivation follow.

## Why It Matters
- A reader who stops after the first sentence of each paragraph should still get the argument
- Claims buried at the end force the reader to re-read the paragraph to find out what it was for
- Generated prose defaults to build-up-then-conclude, which reads as evasive at length

## Correct Approach
- Move the concluding sentence to the front and delete the wind-up
- Keep the delayed claim only when the surprise is the point, which is rare outside narrative writing
- If the paragraph has no claim to promote, it is a candidate for deletion or merging

## Examples

### Weak
```text
There are several factors that influence cache behavior in this setting. Access
patterns vary by workload, and the working set size interacts with the eviction
policy. Prior work has examined some of these factors individually. Taking these
together, we find that eviction policy dominates throughput in our workload.
```

### Strong
```text
Eviction policy dominates throughput in our workload. Access patterns and working
set size matter less because the working set exceeds cache capacity in every
configuration we tested.
```

## Review Guidance
Do not apply this to the first paragraph of a section when it deliberately sets up the section's question, or to transitional paragraphs that exist only to hand off between subsections.
