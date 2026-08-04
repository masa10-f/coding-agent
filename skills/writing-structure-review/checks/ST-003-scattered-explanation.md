# ST-003: Scattered Explanation of One Concept

## Category
Cohesion

## Description
One concept should be explained in one place. Explanations of the same concept spread across several sections should be consolidated.

## Why It Matters
- Scattered explanations drift and eventually contradict each other
- The reader cannot tell which occurrence is authoritative
- This is the most common result of answering review comments by adding text where the comment landed

## Correct Approach
- Identify concepts explained in more than one section
- Choose one authoritative location, usually the first section that depends on the concept
- Replace the other occurrences with a reference, or delete them
- If two occurrences differ, the difference is a content bug: resolve it before consolidating

## Examples

### Weak
```text
2. Introduction - explains the caching strategy in three sentences
4. Architecture - explains the caching strategy again, with a different eviction rule
6. Discussion - explains the caching strategy a third time
```

### Strong
```text
2. Introduction - names the caching strategy, one clause
4. Architecture - the single authoritative explanation
6. Discussion - refers back to Section 4, adds only the new implication
```

## Review Guidance
Scattered explanations are not visible in the heading outline. Search the body for each concept's occurrences and read only enough around each hit to tell an explanation from a mention; that is the exception the phase's input restriction allows. Do not read the sections through.

Deliberate repetition is legitimate in abstracts, introductions, and conclusions. Flag repetition only when the later occurrence re-explains rather than summarizes, or when the two versions disagree.
