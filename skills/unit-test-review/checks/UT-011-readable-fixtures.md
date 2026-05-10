# UT-011: Readable Fixtures

## Category
Fixtures

## Description
Fixtures should be readable and should not hide important setup for the scenario.

## Why It Matters
- Overly broad fixtures make it unclear which inputs matter
- Hidden defaults can cause tests to pass for accidental reasons
- Fixture indirection slows down review and debugging

## Correct Approach
- Keep common fixture setup small and obvious
- Put scenario-specific data in the test body
- Use builders or factories with explicit overrides for important fields
- Avoid shared mutable fixture data

## Examples

### Weak
```python
def test_premium_user_gets_discount(default_user):
    assert discount_for(default_user) == Decimal("10.00")
```

### Strong
```python
def test_premium_user_gets_discount():
    user = make_user(plan="premium", monthly_spend=Decimal("100.00"))

    assert discount_for(user) == Decimal("10.00")
```

## Review Guidance
Flag fixtures when a reader cannot tell why the expected behavior should happen without chasing unrelated setup.
