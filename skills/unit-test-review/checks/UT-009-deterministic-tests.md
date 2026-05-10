# UT-009: Deterministic Tests

## Category
Reliability

## Description
Unit tests should not depend on current time, random state, execution order, local paths, or global mutable state.

## Why It Matters
- Nondeterministic tests erode trust in the test suite
- Order dependence creates failures that are hard to reproduce
- Local environment assumptions break CI and other developers' machines

## Correct Approach
- Inject clocks, random generators, paths, and global dependencies
- Seed randomness only when deterministic examples are sufficient
- Avoid relying on test execution order
- Reset mutated global state in teardown or avoid mutating it

## Examples

### Weak
```python
def test_token_expires_tomorrow():
    token = make_token()
    assert token.expires_at.date() == (datetime.now().date() + timedelta(days=1))
```

### Strong
```python
def test_token_expires_one_day_after_issue_time():
    now = datetime(2026, 1, 1, 12, 0, 0)

    token = make_token(now=now)

    assert token.expires_at == datetime(2026, 1, 2, 12, 0, 0)
```

## Review Guidance
Treat nondeterminism as high priority when it can make the test flaky or environment-specific.
