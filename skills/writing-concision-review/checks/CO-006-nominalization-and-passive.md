# CO-006: Nominalization and Needless Passive

## Category
Sentence Structure

## Description
Turn nominalized verbs back into verbs, and use the active voice unless the agent is genuinely unknown or irrelevant.

## Why It Matters
- Nominalization requires a filler verb, adding words and hiding the action
- The passive voice drops the agent, which is often the fact the reader needs
- Both patterns are the default register of generated technical prose and accumulate quickly

## Correct Approach
- "perform an evaluation of" -> "evaluate", "provide an implementation of" -> "implement", "make a comparison between" -> "compare", "carry out an analysis of" -> "analyze"
- "there was an improvement in X" -> "X improved", "it was observed that X" -> "X"
- Use the passive when the agent is unknown, irrelevant, or when the object is the topic of the paragraph
- Conventional passives in methods sections ("samples were collected") are fine; keep them

## Examples

### Weak
```text
An evaluation of the proposed method was performed, and a comparison with three
baselines was carried out. It was observed that an improvement in accuracy was
achieved.
```

### Strong
```text
We evaluated the proposed method against three baselines. Accuracy improved by 4
points.
```

## Review Guidance
Some venues require the passive voice or forbid the first person. Follow the venue. Nominalization is still worth removing under those constraints; "an evaluation was performed" becomes "the method was evaluated", not "we evaluated the method".
