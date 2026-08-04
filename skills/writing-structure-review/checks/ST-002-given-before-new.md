# ST-002: Given-Before-New Ordering

## Category
Ordering

## Description
A term, definition, or assumption must be introduced before the section that depends on it.

## Why It Matters
- Forward references force the reader to hold undefined terms in memory
- Late definitions are a symptom of sections appended after the fact
- Reordering usually fixes several separate "unclear" comments at once

## Correct Approach
- For each section, list what it assumes the reader already knows
- Locate where each assumption is introduced; if it comes later, move the definition earlier or move the dependent section later
- Prefer moving one definition over repeating it in two places
- Keep forward references only when they are genuinely a roadmap ("Section 5 evaluates this"), not a dependency

## Examples

### Weak
```text
4. Experimental Results - reports scores on the "hard split"
5. Dataset - defines the hard split
```

### Strong
```text
4. Dataset - defines the hard split
5. Experimental Results - reports scores on the hard split
```

## Review Guidance
The heading outline alone will not tell you where a term is defined. Search the body for each term's occurrences and read only enough around each hit to tell a definition from a use; that is the exception the phase's input restriction allows. Do not read the sections through.

Some venues fix the section order. When the order cannot change, propose moving the definition into the earliest dependent section instead, and say that the constraint is the reason.
