# AP-007: Avoid Unnecessary Try-Except Blocks

## Category
Python/Error Handling

## Description
Do not add `try`/`except` blocks unless there is a specific failure mode that must be handled at that point in the code.

## Why It's Bad
- Broad or speculative exception handling hides real bugs
- It makes control flow harder to reason about
- It can convert clear failures into misleading fallback behavior
- It often masks missing knowledge about a dependency or API contract

## Correct Approach
- Prefer direct code when the operation is expected to succeed
- Let unexpected exceptions surface so they can be fixed at the source
- Add exception handling only when the code can recover meaningfully, add context, or translate an expected external failure into a domain-specific result
- When adding a necessary `try`/`except`, document the reason briefly in code review or in a nearby comment if the reason is not obvious

## Examples

### Bad
```python
def load_user_name(user: User) -> str:
    try:
        return user.profile.name
    except Exception:
        return ""
```

### Good
```python
def load_user_name(user: User) -> str:
    return user.profile.name
```

### Acceptable When Recovery Is Explicit
```python
def read_config(path: Path) -> dict[str, str]:
    try:
        raw_config = path.read_text()
    except FileNotFoundError as exc:
        raise ConfigError(f"Config file does not exist: {path}") from exc

    return parse_config(raw_config)
```

## Exceptions

- Boundary code that handles expected external failures, such as missing files, invalid user input, network timeouts, or service-specific errors
- Code that adds domain context while preserving the original exception with `raise ... from exc`
- Cleanup paths where the failure mode is known and the recovery behavior is explicit

If exception handling is necessary, state why it is necessary.
