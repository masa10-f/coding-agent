# EV-003: Terminology Consistency

## Category
Terminology

## Description
One concept, one name. Every term and abbreviation is defined at first use and used consistently thereafter.

## Why It Matters
- Multiple names for one concept make the reader wonder whether they are the same thing
- Synonym variation is introduced by generated text to avoid repetition, which is the wrong goal in technical writing
- Undefined abbreviations are a common artifact of sections written at different times

## Correct Approach
- Build the list of concepts and every surface form used for each
- Pick one name per concept and apply it everywhere, including figure captions, table headers, and code identifiers
- Define each abbreviation at its first occurrence in the body, and again at first occurrence in the abstract
- Repeating the same term is correct; do not vary it for style

## Examples

### Weak
```text
The retrieval module ranks candidates. ... The search component returns the top k.
... The retriever is configured with k=20.
```
Three names, one component.

### Strong
```text
The retriever ranks candidates and returns the top k. ... The retriever is
configured with k=20.
```

## Review Guidance
Distinct names are correct when the concepts are distinct. Before reporting, confirm the surface forms really do refer to one thing; if you cannot tell, that ambiguity is itself the finding.
