# UT-004: Meaningful Assertions

## Category
Assertions

## Description
Assertions should verify the behavior that matters, not merely that code ran.

## Why It Matters
- Smoke assertions can pass while the behavior is broken
- Overly broad assertions miss regressions in important output fields
- Weak tests create false confidence

## Correct Approach
- Assert specific outputs, state changes, calls at external boundaries, or raised errors
- Avoid `assert result`, `assert response`, or `assert not error` when important details are available
- Check error type and relevant message or code when error behavior matters

## Examples

### Weak
```python
def test_create_user():
    user = create_user("ada@example.com")
    assert user
```

### Strong
```python
def test_create_user_sets_email_and_default_status():
    user = create_user("ada@example.com")

    assert user.email == "ada@example.com"
    assert user.status == UserStatus.PENDING
```

## Review Guidance
Prioritize weak assertions that would pass despite realistic regressions. Do not request assertion expansion for incidental fields.
