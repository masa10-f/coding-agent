# RV-002: Defensive Additions

## Category
Revision Behavior

## Description
A comment must be answered by fixing or removing the text, not by adding caveats, footnotes, parenthetical qualifications, or "note that" sentences around it.

## Why It Matters
- Defensive additions leave the original problem in place and add length on top of it
- Accumulated caveats make a document read as evasive even when every individual one is defensible
- This is the most common way an agent responds to criticism: guard the text rather than change it

## Correct Approach
- Identify additions that qualify a claim instead of correcting it
- Replace the qualified claim with the accurate claim
- Move genuine limitations into the limitations section, once, rather than scattering them at each mention
- If the comment revealed that the claim is wrong, delete the claim

## Examples

### Weak
```text
Comment: "This claim is not supported by Table 2."
Revision: "The method improves accuracy (note that results may vary depending on
the dataset and configuration, and further evaluation would be needed to confirm
generality)."
```

### Strong
```text
Revision: "The method improves accuracy by 3 points on the in-domain split
(Table 2). We did not evaluate other domains."
```

## Review Guidance
A limitation stated once in the right place is not a defensive addition. The signal is a qualification attached at the point of criticism that leaves the criticized text unchanged.
