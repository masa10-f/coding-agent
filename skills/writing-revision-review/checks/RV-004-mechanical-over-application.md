# RV-004: Mechanical Over-Application

## Category
Coverage

## Description
A fix applied by pattern match to every superficially similar location, without checking whether each is the same case, is a defect.

## Why It Matters
- Over-application is the overcorrection that follows a comment about under-application
- It damages passages that were correct, and the damage is spread thin enough to be hard to spot
- Removing every hedge, splitting every long sentence, or renaming every occurrence of a string all break meaning somewhere

## Correct Approach
- Check each application site individually against the reason behind the comment
- Look specifically for: hedges removed where uncertainty is real, sentences split where the split repeats the subject, terms renamed inside quotations, code identifiers, or citation titles
- Revert the sites that were already correct, and say why

## Examples

### Weak
```text
Comment: "Too many hedges in Section 3."
Revision: removed every instance of "may", "might", and "possibly" document-wide.
Result: the limitations section now asserts as fact what was correctly uncertain.
```

### Strong
```text
Revision: removed stacked hedges in Section 3 (7 sites). Kept single hedges in
Section 6 (Limitations), where each marks a genuine untested condition.
```

## Review Guidance
The test is not how many sites changed but whether each site's reason matched. Report over-application per site, with the meaning that was lost.
