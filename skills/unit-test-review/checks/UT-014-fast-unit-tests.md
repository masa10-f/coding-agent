# UT-014: Fast Unit Tests

## Category
Performance

## Description
Unit tests should be fast enough to run frequently during development.

## Why It Matters
- Slow unit tests discourage frequent runs
- Slowness often signals hidden integration work, sleeps, retries, or large fixtures
- Slow feedback increases the cost of small changes

## Correct Approach
- Avoid real sleeps, polling loops, and large unnecessary data sets
- Replace time delays with injected clocks or deterministic hooks
- Move slow integration scenarios out of the unit test layer
- Keep performance-sensitive tests focused and bounded

## Examples

### Weak
```python
def test_retry_waits_before_second_attempt():
    start = time.monotonic()
    retry(operation, delay_seconds=5)
    assert time.monotonic() - start >= 5
```

### Strong
```python
def test_retry_uses_configured_delay_before_second_attempt():
    sleeper = FakeSleeper()

    retry(operation, delay_seconds=5, sleep=sleeper.sleep)

    assert sleeper.calls == [5]
```

## Review Guidance
Flag speed issues when they materially slow normal local or CI test runs. Do not require micro-optimizing already fast tests.
