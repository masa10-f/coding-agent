# AP-001: Avoid `object` Type in Python

## Category
Python/Typing

## Description
Do not use `object` as a type annotation in Python. If you need to represent any type, use `typing.Any` instead.

## Why It's Bad
- `object` is the base class of all Python classes, but it's not the same as "any type"
- Using `object` as a type hint is semantically incorrect and can cause type checker confusion
- `object` has a very limited interface, which doesn't reflect the actual usage when you mean "any type"

## Correct Approach
When you need to accept any type:
- Use `typing.Any` to indicate that any type is acceptable
- Consider if a more specific type or generic type parameter would be more appropriate

## Examples

### Bad
```python
def process(data: object) -> object:
    return data

def store_value(value: object) -> None:
    self._value = value
```

### Good
```python
from typing import Any

def process(data: Any) -> Any:
    return data

def store_value(value: Any) -> None:
    self._value = value

# Or better, use generics if applicable
from typing import TypeVar

T = TypeVar('T')

def process(data: T) -> T:
    return data
```
