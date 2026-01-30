# AP-002: Don't Modify pyproject.toml Unnecessarily

## Category
Configuration

## Description
Do not modify `pyproject.toml` without explicit permission. When using suppression syntax like `noqa`, `type: ignore`, or similar, keep the impact as localized as possible.

## Why It's Bad
- `pyproject.toml` changes affect the entire project
- Global linter/type checker rule changes can mask real issues
- Other developers may not be aware of suppressed warnings
- It can lead to technical debt accumulation

## Correct Approach
- Use inline suppression comments instead of global configuration changes
- Scope suppressions to the specific line or block where needed
- Always include a reason for the suppression
- If global changes are truly needed, discuss with the team first

## Examples

### Bad
```toml
# pyproject.toml
[tool.ruff]
ignore = ["E501", "F401"]  # Adding global ignores

[tool.mypy]
disable_error_code = ["import", "attr-defined"]  # Disabling globally
```

### Good
```python
# In the specific file where suppression is needed

# For a specific line
from unused_module import something  # noqa: F401 - Required for side effects

# For type checking issues
result = some_dynamic_call()  # type: ignore[attr-defined] - Dynamic attribute from plugin

# For a specific block
# fmt: off
matrix = [
    [1, 0, 0],
    [0, 1, 0],
    [0, 0, 1],
]
# fmt: on
```
