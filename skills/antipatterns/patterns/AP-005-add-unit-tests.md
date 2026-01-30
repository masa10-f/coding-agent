# AP-005: Always Add Unit Tests for New Features

## Category
Testing

## Description
When adding new functionality to the codebase, always include corresponding unit tests that verify the new feature works correctly.

## Why It's Bad
- Untested code is unreliable code
- Bugs may go unnoticed until production
- Future refactoring becomes risky without tests
- Other developers can't verify their changes don't break the feature
- Code coverage decreases over time

## Correct Approach
1. Write tests for all new functions, methods, and classes
2. Test both happy paths and edge cases
3. Include error handling tests
4. Follow the existing test structure and conventions in the project
5. Ensure tests are independent and can run in any order

## Examples

### Bad
```python
# file: services/calculator.py
def calculate_discount(price: float, discount_percent: float) -> float:
    """Calculate discounted price."""
    if discount_percent < 0 or discount_percent > 100:
        raise ValueError("Discount must be between 0 and 100")
    return price * (1 - discount_percent / 100)

# No tests added!
```

### Good
```python
# file: services/calculator.py
def calculate_discount(price: float, discount_percent: float) -> float:
    """Calculate discounted price."""
    if discount_percent < 0 or discount_percent > 100:
        raise ValueError("Discount must be between 0 and 100")
    return price * (1 - discount_percent / 100)
```

```python
# file: tests/services/test_calculator.py
import pytest
from services.calculator import calculate_discount


class TestCalculateDiscount:
    """Tests for calculate_discount function."""

    def test_calculate_discount_basic(self):
        """Test basic discount calculation."""
        assert calculate_discount(100, 10) == 90.0

    def test_calculate_discount_zero_discount(self):
        """Test with no discount."""
        assert calculate_discount(100, 0) == 100.0

    def test_calculate_discount_full_discount(self):
        """Test with 100% discount."""
        assert calculate_discount(100, 100) == 0.0

    def test_calculate_discount_negative_raises(self):
        """Test that negative discount raises ValueError."""
        with pytest.raises(ValueError, match="Discount must be between 0 and 100"):
            calculate_discount(100, -10)

    def test_calculate_discount_over_100_raises(self):
        """Test that discount over 100 raises ValueError."""
        with pytest.raises(ValueError, match="Discount must be between 0 and 100"):
            calculate_discount(100, 150)
```

## Test Checklist

When adding new features, ensure you have tests for:

- [ ] Normal/expected inputs (happy path)
- [ ] Boundary values (min, max, empty)
- [ ] Invalid inputs (error cases)
- [ ] Edge cases specific to the feature
- [ ] Integration with other components (if applicable)
