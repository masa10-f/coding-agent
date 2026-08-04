# FL-002: Connective Matches the Actual Logic

## Category
Logic

## Description
Connectives such as "therefore", "thus", "however", and "in contrast" must reflect a relationship that actually holds between the two statements.

## Why It Matters
- False connectives simulate reasoning without performing it, which is hard to spot at speed
- A reader who trusts the connective accepts an inference the text never made
- Wrong connectives usually mark the seam where text was inserted

## Correct Approach
- For each connective, state the relationship it asserts and verify it against the two statements
- If the relationship does not hold, either supply the missing step or replace the connective with a neutral one
- Delete connectives that assert nothing: "also", "additionally", "furthermore", "moreover" stacked between unrelated points

## Examples

### Weak
```text
The model was trained on 8 GPUs for 12 hours. Therefore, the approach is
practical for small teams.
```
"Therefore" asserts a causal step that is missing: no cost, availability, or baseline comparison is given.

### Strong
```text
The model was trained on 8 GPUs for 12 hours, roughly $40 of rented compute at
current prices. That cost is within reach of a small team.
```

### Weak
```text
The proposed method is faster than the baseline. In contrast, it is also more
accurate.
```
"In contrast" asserts opposition, but both statements are improvements.

### Strong
```text
The proposed method is both faster and more accurate than the baseline.
```

## Review Guidance
Report the missing inferential step, not just the wrong word. Replacing "therefore" with "and" hides the gap instead of fixing it.
