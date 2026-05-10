# UT-012: Meaningful Test Data

## Category
Test Data

## Description
Test data should be minimal, realistic, and meaningful for the behavior under test.

## Why It Matters
- Random or placeholder values can hide which inputs matter
- Oversized fixtures make tests harder to read
- Unrealistic data can miss real parsing, validation, or domain behavior

## Correct Approach
- Use the smallest data set that proves the behavior
- Choose values that make the scenario obvious
- Use realistic examples when format, validation, or domain meaning matters
- Avoid irrelevant fields unless the unit requires them

## Examples

### Weak
```python
def test_format_name():
    assert format_name({"first": "foo", "last": "bar", "age": 999}) == "foo bar"
```

### Strong
```python
def test_format_name_combines_first_and_last_name():
    assert format_name({"first": "Ada", "last": "Lovelace"}) == "Ada Lovelace"
```

## Review Guidance
Treat poor data as a review issue when it obscures intent or risks missing realistic failures. Do not nitpick harmless placeholder data.
