# CO-004: Stacked Hedging

## Category
Hedging

## Description
One hedge per claim. Stacked hedges make a statement unfalsifiable without making it more honest.

## Why It Matters
- "May potentially suggest" claims nothing and cannot be wrong
- Stacked hedging is the most recognizable signature of generated academic prose
- Genuine uncertainty is better expressed by stating its source and size

## Correct Approach
- Keep at most one hedge per claim
- Prefer a stated bound to a hedge: "within one standard deviation" beats "may be somewhat"
- Where the uncertainty is real, name it: sample size, single seed, one dataset
- Delete the hedge entirely when the document elsewhere states the result as fact

## Examples

### Weak
```text
These results may potentially suggest that the approach could be somewhat more
effective in certain settings, although it is possible that other factors might
also play a role.
```

### Strong
```text
The approach outperforms the baseline on both datasets. We ran a single seed, so
the 2-point gap on the smaller dataset may not be reliable.
```

## Review Guidance
Do not strip hedges from claims the evidence genuinely does not support. Converting an over-hedged weak claim into a confident false one is worse than the original. When in doubt, replace the hedge stack with a single hedge plus its reason.

Which hedges are required is the output of `writing-evidence-review` (phase 3). Where that phase has run, keep the hedges and scope statements it required and cut only the surplus. Where it has not, do not decide the question here: reduce the stack to the single strongest hedge, and defer the choice of which claims may be stated flatly.
