# CO-001: Meta-Sentences and Preamble

## Category
Padding

## Description
Sentences that announce what the text is about to do, rather than doing it, should be deleted.

## Why It Matters
- Headings already tell the reader what a section covers
- Announcing an argument delays it and signals padding
- These sentences are generated automatically and almost never carry information

## Correct Approach
- Delete announcements: "This section describes...", "In what follows we will...", "It is worth noting that...", "Before presenting X, it is important to understand Y", "As can be seen below"
- Delete restated headings at the top of a section
- Keep a roadmap sentence only in a long introduction where it genuinely orients the reader

## Examples

### Weak
```text
In this section, we describe the evaluation methodology. Before presenting the
results, it is important to first understand how the benchmarks were selected.
We selected benchmarks that stress the retrieval path.
```

### Strong
```text
We selected benchmarks that stress the retrieval path.
```

## Review Guidance
Keep the roadmap paragraph at the end of a paper's introduction if the venue expects it. Delete the per-section copies of it.
