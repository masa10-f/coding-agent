# UT-015: Actionable Failure Output

## Category
Debugging

## Description
Test failures should make the problem quick to identify.

## Why It Matters
- Ambiguous failures waste debugging time
- Loops with bare assertions hide which case failed
- Custom assertion messages can help when default output lacks context

## Correct Approach
- Prefer assertion helpers that show useful diffs
- Use parametrized test IDs or case labels when many cases share a test
- Include focused custom messages only when default assertion output is insufficient
- Avoid catching assertion errors or replacing useful framework output

## Examples

### Weak
```python
def test_slug_cases():
    for raw, expected in cases:
        assert slugify(raw) == expected
```

### Strong
```python
@pytest.mark.parametrize(
    ("raw", "expected"),
    [
        pytest.param("Hello World", "hello-world", id="spaces"),
        pytest.param("Hello---World!!!", "hello-world", id="punctuation"),
    ],
)
def test_slugify_normalizes_common_separators(raw, expected):
    assert slugify(raw) == expected
```

## Review Guidance
Flag failure-output issues when a realistic failure would not identify the broken scenario quickly.
