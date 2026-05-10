# UT-005: Explicit Expected Values

## Category
Assertions

## Description
Expected values should be explicit and independent from the implementation being tested.

## Why It Matters
- Recomputing expected values with the same logic can copy the bug into the test
- Dynamic expectations can make regressions look correct
- Explicit examples are easier to review and debug

## Correct Approach
- Use literal expected values for representative examples
- Compute expected values only with an independent, simpler oracle
- Avoid deriving expectations by calling the same unit or private helpers under test

## Examples

### Weak
```python
def test_discount():
    price = 100
    percent = 15

    assert apply_discount(price, percent) == price * (1 - percent / 100)
```

### Strong
```python
def test_apply_discount_subtracts_percentage_from_price():
    assert apply_discount(100, 15) == 85
```

## Review Guidance
Flag computed expectations when they duplicate the production algorithm. Simple independent calculations are acceptable when they make a complex expected value readable.
