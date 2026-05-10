# UT-002: Arrange-Act-Assert Structure

## Category
Readability

## Description
Tests should make setup, action, and verification easy to distinguish.

## Why It Matters
- Mixed setup and assertions make the tested behavior unclear
- Hidden actions inside assertions make failures harder to interpret
- Clear structure reduces accidental testing of the wrong behavior

## Correct Approach
- Arrange only the data, fixtures, and dependencies needed for the scenario
- Act once when practical, assigning the result to a meaningful variable
- Assert the expected observable behavior
- Use comments or whitespace only when they improve readability

## Examples

### Weak
```python
def test_total():
    assert invoice_total([LineItem("book", 2, 10)]) == 20
```

### Strong
```python
def test_invoice_total_multiplies_quantity_by_unit_price():
    items = [LineItem(name="book", quantity=2, unit_price=10)]

    total = invoice_total(items)

    assert total == 20
```

## Review Guidance
Do not require formal `# Arrange`, `# Act`, `# Assert` comments. The concern is whether the behavior is readable and the action under test is clear.
