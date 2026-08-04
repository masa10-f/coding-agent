# EV-006: Citations Support What They Are Cited For

## Category
Citation

## Description
A cited work must actually establish the claim it is attached to, and the attachment point must be the claim it supports.

## Why It Matters
- A citation that does not support its claim is worse than no citation: it looks checked
- Generated text attaches plausible references to plausible claims without verifying the match
- Citation drift accumulates when text is edited around fixed reference markers

## Correct Approach
- For each citation, state what the cited work shows and how it relates to the claim
- Distinguish "this work reports X" from "this work is related to X"
- Verify the citation is attached to the sentence it supports, not the neighboring one
- Flag any reference you cannot verify rather than assuming the match holds

## Examples

### Weak
```text
Transformer models are known to degrade under distribution shift [7].
```
[7] is an architecture paper that never measures distribution shift.

### Strong
```text
Transformer classifiers lose 12-18 points of accuracy under domain shift on three
benchmarks [7].
```

## Review Guidance
When you cannot access a reference, say so explicitly and mark the claim as unverified. Do not silently accept the citation, and do not report it as wrong.
