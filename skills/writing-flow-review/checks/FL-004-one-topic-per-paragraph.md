# FL-004: One Topic Per Paragraph

## Category
Scope

## Description
A paragraph should make one claim. A paragraph whose claim needs two clauses to state is a split candidate.

## Why It Matters
- Multi-topic paragraphs hide the second topic from a skimming reader
- They usually result from appending a new point to the nearest existing paragraph
- Splitting them exposes ordering problems that were previously invisible

## Correct Approach
- Split so that each resulting paragraph leads with its own claim
- After splitting, check the order: the second half often belongs elsewhere in the section
- Merge in the opposite case, where consecutive short paragraphs make one claim between them

## Examples

### Weak
```text
The retrieval step uses BM25 with default parameters, which we found sufficient
for the corpus size. We also changed the tokenizer to preserve hyphenated terms,
since the domain vocabulary contains many compound identifiers, and this raised
recall by 4 points on the validation split.
```

### Strong
```text
The retrieval step uses BM25 with default parameters, which were sufficient at
this corpus size.

The tokenizer preserves hyphenated terms because the domain vocabulary is full of
compound identifiers. This raised validation recall by 4 points.
```

## Review Guidance
Do not split a paragraph whose sentences jointly establish one claim, even when it runs long. Length alone is not the trigger; a second independent claim is.
