# FL-005: Bullet Lists Used to Avoid Arguing

## Category
Argument

## Description
A bullet list places items side by side without stating their relationship. Where the text needs to argue, weigh, or sequence, prose is required.

## Why It Matters
- Lists let the writer skip the hard part: which item matters most and why
- Generated text reaches for lists exactly where the reasoning is thinnest
- Readers cannot infer priority, causality, or trade-offs from a bullet

## Correct Approach
- Keep lists for genuinely parallel, unordered items: options, requirements, parameters, steps
- Convert to prose when the items are causes, trade-offs, or an argument's steps
- If the list must stay, add a preceding sentence that states the relationship the list cannot

## Examples

### Weak
```text
The performance regression has several causes:
- The cache was disabled in the new configuration
- The dataset grew by 30%
- The serialization format changed
```

### Strong
```text
The disabled cache accounts for nearly all of the regression: re-enabling it
recovers 90% of the lost throughput. The 30% dataset growth and the new
serialization format together account for the rest.
```

## Review Guidance
Do not flag lists in reference material, API documentation, checklists, or configuration tables, where side-by-side presentation is the correct form.
