# ST-001: Every Section Earns Its Place

## Category
Purpose

## Description
Each section must have a statable contribution to the document's main claim. If its contribution cannot be written in one sentence, the section is a merge or delete candidate.

## Why It Matters
- Sections added in response to review comments often survive without ever being integrated
- A reader cannot tell which sections are load-bearing when several are decorative
- Padding sections dilute the claim and lengthen review cycles

## Correct Approach
- State each section's contribution as "This section establishes X, which the claim needs because Y"
- Merge sections whose contributions are the same
- Delete sections that only restate what an earlier section established
- Move background that supports one specific argument into that argument's section

## Examples

### Weak
```text
3. Related Work
4. Background on Transformers
5. Preliminaries
6. Proposed Method
```
Sections 3-5 have overlapping, unstated contributions. "Background" and "Preliminaries" cannot be distinguished from their headings.

### Strong
```text
3. Related Work - positions the method against the two closest prior approaches
4. Preliminaries - defines the notation and the two operators used in Section 5
5. Proposed Method - the contribution
```
Transformer background was cut because the paper's claim does not depend on it.

## Review Guidance
A section can be load-bearing without being novel. Do not flag standard required sections such as Method, Results, or Limitations merely because their content is conventional. Flag them only when their actual content does not serve the stated purpose.
