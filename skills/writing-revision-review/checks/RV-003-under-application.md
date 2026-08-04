# RV-003: Under-Application to Sibling Occurrences

## Category
Coverage

## Description
When a comment names one instance of a pattern, every other instance of the same pattern must be checked and either fixed or explicitly exempted.

## Why It Matters
- Reviewers cite one example and expect the class to be fixed
- Fixing only the cited line produces a document that is now internally inconsistent, which is worse than uniform imperfection
- It also guarantees another review round for the same issue

## Correct Approach
- Read each comment as naming a class, unless it says otherwise
- Enumerate the other occurrences and list them explicitly
- Fix them, or state per occurrence why it is exempt
- Terminology, notation, hedging, and unit conventions are the classes where this fails most often

## Examples

### Weak
```text
Comment: "Section 4 calls it 'the retriever' but Section 2 says 'search module'."
Revision: changed the one occurrence in Section 4.
Result: five other occurrences of "search module" remain in Sections 5 and 6.
```

### Strong
```text
Revision: standardized on "retriever" across all 11 occurrences, including Figure
3's caption and Table 2's header. The identifier `search_module` in the code
listing is unchanged, since it is the actual class name.
```

## Review Guidance
Confirm the other occurrences really are the same pattern before requiring the fix. A term used in a different sense, or a hedge that the evidence genuinely requires, is an exemption to state, not an instance to fix.
