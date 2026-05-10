# UT-007: Regression Tests for Bug Fixes

## Category
Coverage

## Description
A bug fix should include a test that fails before the fix and passes after it when practical.

## Why It Matters
- Without a regression test, the same bug can silently return
- A targeted regression test documents the exact failure mode
- Bug fixes often touch subtle behavior not covered by happy-path tests

## Correct Approach
- Reproduce the reported input, state, or workflow as narrowly as possible
- Assert the corrected externally visible behavior
- Include the bug's edge condition, not just a nearby happy path
- If a regression test is impractical, explain why in the review

## Examples

### Weak
```python
def test_slugify():
    assert slugify("Hello World") == "hello-world"
```

### Strong
```python
def test_slugify_collapses_repeated_separators_from_punctuation():
    assert slugify("Hello---World!!!") == "hello-world"
```

## Review Guidance
Raise this as high priority when the change is explicitly a bug fix and no test would have caught the original failure.
