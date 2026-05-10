# UT-003: One Behavior Per Test

## Category
Scope

## Description
Each unit test should check one behavior or one scenario.

## Why It Matters
- Multi-scenario tests obscure which behavior failed
- Large tests often stop at the first failure and hide additional regressions
- Unrelated assertions make tests harder to maintain

## Correct Approach
- Split unrelated scenarios into separate tests
- Keep closely related assertions together when they describe one observable result
- Use parametrization for the same behavior across multiple inputs

## Examples

### Weak
```python
def test_validate_email():
    assert validate_email("a@example.com") is True
    assert validate_email("missing-at") is False
    assert normalize_email(" A@EXAMPLE.COM ") == "a@example.com"
```

### Strong
```python
def test_validate_email_accepts_address_with_domain():
    assert validate_email("a@example.com") is True


def test_validate_email_rejects_address_without_at_symbol():
    assert validate_email("missing-at") is False
```

## Review Guidance
Do not split tests when multiple assertions are necessary to verify one returned object, one state transition, or one error result.
