# EV-001: Every Claim Names Its Evidence

## Category
Support

## Description
Each assertion must point to its support: a number in the document, a figure or table, a derivation, or a citation. Assertions with no locatable support are findings.

## Why It Matters
- Well-formed sentences read as supported even when nothing backs them
- Unsupported claims are the failure mode that invalidates a document, unlike style issues
- Generated text produces confident summary sentences that no measurement in the document justifies

## Correct Approach
- For each claim, write where the support is: "Table 2, row 3", "Section 4.1", "[12]"
- If the support does not exist, choose one: measure it, weaken the claim to what is shown, or delete it
- Do not repair an unsupported claim by adding a hedge; an unfalsifiable claim is not an improvement

## Examples

### Weak
```text
The proposed method scales well to larger corpora and remains robust under
distribution shift.
```
Neither scaling nor shift is measured anywhere in the document.

### Strong
```text
Throughput stays within 8% of baseline as the corpus grows from 1M to 10M
documents (Table 3). We did not evaluate distribution shift.
```

## Review Guidance
Common knowledge in the field does not need a citation. The line is whether a reader of the document could check the claim. If the claim is central to the contribution, it needs support even when it is well known.
