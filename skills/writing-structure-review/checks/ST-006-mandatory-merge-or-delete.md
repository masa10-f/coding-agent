# ST-006: Mandatory Merge or Delete Candidate

## Category
Review Discipline

## Description
The review must name at least one section as a merge or delete candidate, or list every section's justification for existing.

## Why It Matters
- Reviews that only add scope let documents grow without bound
- Documents that grew by appending almost always contain a redundant section
- Forcing the search for one deletion surfaces structural redundancy that comment-by-comment review misses

## Correct Approach
- For each section, ask what breaks if it is removed
- Nominate the section whose removal costs the least, and say where its surviving content goes
- If nothing can be removed, state per section what breaks without it

## Examples

### Weak
```text
All sections are necessary.
```

### Strong
```text
Delete candidate: Section 5 (Discussion). Its first paragraph repeats Section 4.3; its second is the only new content and moves into Section 6 (Limitations). Removing it costs nothing.
```

### Strong (nothing removable)
```text
No merge or delete candidate.
2 Setup - removing it leaves the notation in Section 3 undefined
3 Method - the contribution
4 Results - removing it leaves the claim unsupported
5 Limitations - removing it leaves the claim unbounded
```

## Review Guidance
Do not nominate a section that a venue or template requires. Nominate content within it instead, and say the section header must stay.
