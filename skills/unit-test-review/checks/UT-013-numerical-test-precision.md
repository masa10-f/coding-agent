# UT-013: Numerical Test Precision

## Category
Numerical Code

## Description
Tests for numerical code should check dtype, shape, units, axis order, and tolerances when those properties are part of correctness.

## Why It Matters
- Numerical code can return plausible values with wrong shape or axes
- Exact equality can make floating-point tests brittle
- Missing unit or dtype checks can hide serious downstream bugs

## Correct Approach
- Assert shape and dtype for arrays, tensors, or tabular numerical outputs
- Assert units and axis order when the domain depends on them
- Use appropriate tolerances for floating-point comparisons
- Include representative boundary values such as zeros, negatives, NaN, or empty arrays when relevant

## Examples

### Weak
```python
def test_normalize():
    result = normalize(values)
    assert result.sum() == 1.0
```

### Strong
```python
def test_normalize_returns_float_vector_with_unit_sum():
    result = normalize(np.array([1, 1, 2], dtype=np.int64))

    assert result.dtype == np.float64
    assert result.shape == (3,)
    np.testing.assert_allclose(result, np.array([0.25, 0.25, 0.5]), rtol=1e-12)
```

## Review Guidance
Only apply this check to numerical behavior. Do not demand dtype, shape, or tolerance assertions for ordinary scalar business logic.
