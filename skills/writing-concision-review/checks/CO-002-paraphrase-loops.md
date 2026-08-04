# CO-002: Paraphrase Loops

## Category
Redundancy

## Description
Stating the same content twice in different words adds length without adding information. Keep the more precise version and delete the other.

## Why It Matters
- The reader searches the second version for the new information it does not contain
- Paraphrase is the default way generated text reaches a target length
- Two versions of one claim eventually drift apart during editing

## Correct Approach
- Look for "that is", "in other words", "put differently", "this means that" and check whether the restatement adds anything
- Keep the version with concrete nouns and numbers; delete the abstract one
- A restatement is legitimate when it converts formalism into intuition, or the reverse, for a reader who needs both

## Examples

### Weak
```text
The scheduler prioritizes short jobs. In other words, jobs with lower estimated
runtime are placed ahead of longer ones in the queue. This means that a job's
position depends on how long it is expected to run.
```

### Strong
```text
The scheduler places jobs in the queue by ascending estimated runtime.
```

## Review Guidance
A formal statement followed by a plain-language gloss is not a paraphrase loop when the audience needs both. Two plain-language versions of the same statement always are.
