# AP-009: Avoid Careless Use of `cast`

## Category
Python/Typing

## Description
Do not use `typing.cast` or equivalent casting helpers just to silence a type checker. A cast does not validate data at runtime, so it must only be used when the type relationship is already guaranteed by surrounding code and cannot be expressed naturally.

If there is no natural implementation that avoids the cast, get explicit user approval before adding it.

## Why It's Bad
- `cast` can hide real type bugs by overriding the type checker without changing runtime behavior
- It makes future refactors riskier because the asserted type can drift away from reality
- It often bypasses better designs such as narrowing, validation, typed helpers, generics, overloads, or improved annotations
- Repeated casts make code harder to trust and review

## Correct Approach
Before using `cast`:
- Use normal type narrowing with `isinstance`, `issubclass`, sentinel checks, `TypeGuard`, or `TypeIs`
- Improve the source annotation so the correct type flows naturally
- Introduce a small typed helper, generic, overload, protocol, or dataclass/model when that reflects the domain
- Validate untyped external data at the boundary and return a properly typed value
- Follow existing project patterns for third-party library typing gaps

Only use `cast` after these alternatives have been considered and rejected. When a cast is still necessary, keep it local, document the invariant briefly, and obtain explicit user approval first.

## Examples

### Bad
```python
from typing import cast

def first_name(payload: dict[str, object]) -> str:
    return cast(str, payload["name"])
```

### Good
```python
def first_name(payload: dict[str, object]) -> str:
    name = payload["name"]
    if not isinstance(name, str):
        raise TypeError("name must be a string")
    return name
```

### Cast Only With Approval
```python
from typing import cast

def get_plugin(config: Config) -> Plugin:
    plugin = config.registry["default"]
    # Approved: registry is populated exclusively from Plugin instances during startup.
    return cast(Plugin, plugin)
```

## Exceptions

- A cast may be acceptable for a documented third-party typing bug or a framework API whose runtime contract is stronger than its stubs
- A cast may be acceptable after runtime validation has already happened elsewhere in the same control flow
- Even in these cases, the user must approve the cast before it is introduced when no natural cast-free implementation exists
