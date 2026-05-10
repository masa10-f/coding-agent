# UT-008: Isolated External Boundaries

## Category
Isolation

## Description
Unit tests should avoid real network calls, databases, external APIs, and persistent filesystem writes.

## Why It Matters
- External dependencies make tests slow and flaky
- Tests can fail for reasons unrelated to the code under review
- Persistent writes can pollute local or CI environments

## Correct Approach
- Replace external services with fakes, stubs, or boundary mocks
- Use temporary directories for filesystem behavior that must be tested
- Keep real integration behavior in integration tests, not unit tests
- Assert the boundary interaction only when it is part of the unit contract

## Examples

### Weak
```python
def test_fetch_profile():
    profile = fetch_profile("https://api.example.com/users/1")
    assert profile["id"] == 1
```

### Strong
```python
def test_fetch_profile_parses_client_response():
    client = FakeClient(response={"id": 1, "name": "Ada"})

    profile = fetch_profile(client, user_id=1)

    assert profile == {"id": 1, "name": "Ada"}
```

## Review Guidance
Flag real external access in unit tests unless the project clearly marks the test as integration or end-to-end.
