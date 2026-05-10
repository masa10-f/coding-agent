# UT-006: Relevant Edge Cases

## Category
Coverage

## Description
Tests should cover edge cases when they are relevant to correctness or regression risk.

## Why It Matters
- Boundary behavior often contains real bugs
- Missing edge cases can leave important branches unprotected
- Demanding every possible edge case wastes time on low-risk scenarios

## Correct Approach
- Add edge cases for boundaries, empty inputs, invalid inputs, rounding, parsing ambiguity, permissions, and error paths when they matter
- Prefer a small number of high-value cases over exhaustive matrices
- Match edge cases to the unit's contract and past bugs

## Examples

### Missing
```python
def test_chunk_items_splits_items_into_groups():
    assert chunk_items([1, 2, 3, 4], size=2) == [[1, 2], [3, 4]]
```

### Better
```python
def test_chunk_items_keeps_remainder_group_when_items_do_not_divide_evenly():
    assert chunk_items([1, 2, 3], size=2) == [[1, 2], [3]]
```

## Review Guidance
Suggest only edge cases that are likely to catch bugs in the changed behavior. Do not ask for broad coverage checklists.
