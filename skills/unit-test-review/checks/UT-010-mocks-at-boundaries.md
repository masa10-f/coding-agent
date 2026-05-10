# UT-010: Mocks Only at External Boundaries

## Category
Mocking

## Description
Mocks should be used primarily for external boundaries, not for internal implementation details.

## Why It Matters
- Mocking internals couples tests to how code is written instead of what it does
- Refactors can break tests even when behavior is unchanged
- Over-mocking can hide broken integration between local units

## Correct Approach
- Mock network clients, databases, message queues, clocks, random generators, and other external boundaries
- Prefer real local collaborators when they are fast and deterministic
- Assert observable behavior before call counts
- Assert calls only when the interaction is the behavior being tested

## Examples

### Weak
```python
def test_report_total(mocker):
    calculate = mocker.patch("reports.calculate_total", return_value=42)

    assert build_report([1, 2, 3]).total == 42
    calculate.assert_called_once()
```

### Strong
```python
def test_build_report_includes_total_for_items():
    report = build_report([LineItem("book", 2, 10)])

    assert report.total == 20
```

## Review Guidance
Do not reject every mock. Focus on mocks that make the test fragile or prevent real behavior from being verified.
