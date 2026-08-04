# CO-005: One Idea Per Sentence

## Category
Sentence Structure

## Description
Split sentences that carry more than one idea, nest two or more embedded clauses, or separate the subject from its verb by a long span.

## Why It Matters
- Nested clauses force the reader to hold the sentence open while parsing an aside
- A subject separated from its verb by a long span makes the reader re-read to find what was asserted
- Long sentences hide missing logical steps between their clauses

## Correct Approach
- One assertion per sentence; move qualifications into their own sentence
- Cap embedding at one level
- Keep the subject close to its verb; move long qualifying clauses out of the gap between them
- After splitting, check the order: the second sentence sometimes belongs before the first

## Examples

### Weak
```text
Although the baseline, which was trained on the same corpus that we used for the
proposed model but without the augmentation step that we describe in Section 3,
performs comparably on the in-domain split, it degrades out of domain.
```

### Strong
```text
The baseline was trained on the same corpus as the proposed model, without the
augmentation described in Section 3. It matches the proposed model in domain and
degrades out of domain.
```

### Weak
```text
The proposed method, by relaxing the distributional assumption that prior work
relied on, is able to limit the accuracy degradation that occurs when the
distribution shifts, which happens frequently in production settings.
```

### Strong
```text
The proposed method makes no distributional assumption. Accuracy therefore
degrades less under the distribution shifts common in production.
```

## Review Guidance
Length alone is not the trigger. A long sentence with one assertion and no nesting is fine. Do not split a sentence when the split forces you to repeat the subject three times.
