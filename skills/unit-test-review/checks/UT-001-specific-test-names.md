# UT-001: Specific Test Names

## Category
Naming

## Description
Test names should identify the unit, scenario, and expected behavior.

## Why It Matters
- Vague names make failures slower to triage
- Generic names hide duplicated or missing scenarios
- A useful name lets readers understand intent before reading setup

## Correct Approach
- Name the unit or behavior under test
- Include the scenario or input condition
- Include the expected result
- Prefer behavior language over implementation steps

## Examples

### Weak
```python
def test_parser():
    assert parse_user("Ada <ada@example.com>")
```

### Strong
```python
def test_parse_user_returns_name_and_email_for_valid_contact_string():
    assert parse_user("Ada <ada@example.com>") == {
        "name": "Ada",
        "email": "ada@example.com",
    }
```

## Review Guidance
Flag vague names only when they make the test intent or failure hard to understand. Do not require renaming merely to match a preferred naming style.
