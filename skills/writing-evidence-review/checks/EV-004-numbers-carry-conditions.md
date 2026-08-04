# EV-004: Numbers Carry Their Conditions

## Category
Measurement

## Description
A reported number must state its unit, its baseline or comparison point, and the conditions under which it was measured.

## Why It Matters
- A percentage without a baseline is uninterpretable and often overstates the result
- Missing conditions make the number unreproducible, which is the same as unsupported
- Relative improvements are used to make small absolute differences look large

## Correct Approach
- Give the unit, the absolute values, and the relative change where relative change is meaningful
- State the conditions the number depends on: hardware, dataset, sample size, number of runs, variance
- Name the comparison point explicitly; "2x faster" needs to say faster than what
- Keep significant figures consistent with the measurement precision

## Examples

### Weak
```text
Our optimization improves performance by 40% and reduces memory usage
significantly.
```

### Strong
```text
Median query latency drops from 210 ms to 126 ms (40%) on a single c6i.4xlarge,
over 1,000 queries. Peak RSS falls from 3.1 GB to 2.4 GB.
```

## Review Guidance
Not every number needs full experimental conditions. Apply this in proportion to how load-bearing the number is: headline results in the abstract and results section need the full set, incidental figures do not.
