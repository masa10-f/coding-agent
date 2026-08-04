# CO-003: Empty Abstractions

## Category
Specificity

## Description
Phrases that describe importance, variety, or degree without naming anything should be replaced with the specific noun, number, or mechanism, or deleted.

## Why It Matters
- These phrases read as content but survive any substitution, which means they say nothing
- They are how generated text fills space when the specific fact is not available
- Replacing them either produces real content or reveals that there is none

## Correct Approach
- Test each phrase by substitution: if "significant" could be replaced by "modest" without contradicting anything in the document, the word is empty
- Replace with the measurement, the mechanism, or the named item
- If the specific fact is unknown, delete the sentence rather than keeping the vague version
- Common offenders: "plays an important role", "significant improvement", "various factors", "a number of", "leverages", "robust", "a wide range of", "substantially", "effectively", "state-of-the-art performance"

## Examples

### Weak
```text
Caching plays an important role in system performance, and various factors
contribute to a significant improvement in throughput.
```

### Strong
```text
Enabling the cache raises throughput from 1.2k to 4.8k requests per second.
```

## Review Guidance
Abstractions are correct in an abstract or introduction that deliberately withholds detail available later. Flag them when the specific version exists elsewhere in the document, or when no specific version exists at all.

`writing-evidence-review` (phase 3) has already located each claim's supporting number or artifact. Use its output to find the replacement value rather than searching again, and where it recorded that no support exists, delete the sentence instead of substituting a specific figure you cannot source.
