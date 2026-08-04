# EV-002: Claim Strength Matches the Evidence

## Category
Calibration

## Description
The scope of a claim must not exceed the scope of the evidence. Results on one dataset, one seed, or one workload support claims about that dataset, seed, or workload.

## Why It Matters
- Over-generalization is harder to catch than a missing citation because the evidence exists
- Abstracts and conclusions drift stronger than the results section they summarize
- Reviewers reject over-claiming faster than they reject a modest result

## Correct Approach
- Compare each claim against the conditions actually tested: how many datasets, seeds, sizes, languages, hardware configurations
- Restate the claim with its scope attached rather than deleting it
- Check the abstract and conclusion against the results section specifically; that is where drift concentrates

## Examples

### Weak
```text
Our method is more sample-efficient than reinforcement learning.
```
Evidence: one task, one RL baseline, three seeds.

### Strong
```text
On the navigation task, our method reaches the target success rate with 40% fewer
episodes than PPO (3 seeds, Figure 4). We did not test other task families or
other RL algorithms.
```

### Weak
```text
The method is effective in production settings.
```
Evidence: an offline benchmark only.

### Strong
```text
The method outperforms the baseline on our offline benchmark. We have not
deployed it or measured it in production.
```

## Review Guidance
Stating the limit is not weakening the contribution; it is what makes the claim checkable. Do not resolve over-claiming by adding hedges such as "may" while leaving the scope unstated.
