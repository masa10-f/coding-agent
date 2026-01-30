# AP-006: Use Generic Types for Input, Concrete Types for Output

## Category
Python/Typing

## Description
Function parameters (input) should use abstract generic types like `Mapping`, `Sequence`, `Iterable` from `collections.abc`, while return types (output) should use concrete types like `dict`, `list`, `set`.

## Why It's Bad
- Using concrete types for input limits flexibility unnecessarily
- Using abstract types for output makes it unclear what the caller will receive
- Functions that accept only `list` can't be called with tuples or other sequences
- Functions that return `Sequence` force callers to handle unknown concrete types

## Correct Approach
- **Input parameters**: Use abstract types (`Mapping`, `Sequence`, `Iterable`, etc.)
  - Allows callers to pass any compatible type
  - Follows the "be liberal in what you accept" principle
- **Return types**: Use concrete types (`dict`, `list`, `set`, etc.)
  - Makes it clear what the caller will receive
  - Follows the "be conservative in what you return" principle

## Examples

### Bad
```python
# Too restrictive input - only accepts list
def process_items(items: list[str]) -> list[str]:
    return [item.upper() for item in items]

# Too vague output - caller doesn't know concrete type
from collections.abc import Sequence, Mapping

def get_user_data(user_id: int) -> Mapping[str, str]:
    return {"name": "John", "email": "john@example.com"}

def filter_items(items: Sequence[int]) -> Sequence[int]:
    return [x for x in items if x > 0]
```

### Good
```python
from collections.abc import Sequence, Mapping, Iterable

# Abstract input, concrete output
def process_items(items: Sequence[str]) -> list[str]:
    return [item.upper() for item in items]

def get_user_data(user_id: int) -> dict[str, str]:
    return {"name": "John", "email": "john@example.com"}

def filter_items(items: Iterable[int]) -> list[int]:
    return [x for x in items if x > 0]

# Now these all work:
process_items(["a", "b", "c"])      # list
process_items(("a", "b", "c"))      # tuple
process_items(x for x in "abc")     # generator (with Iterable)
```

## Quick Reference

| Input Type | Use For | Output Type |
|------------|---------|-------------|
| `Sequence[T]` | Ordered, indexable collections | `list[T]` |
| `Mapping[K, V]` | Key-value mappings | `dict[K, V]` |
| `Iterable[T]` | Any iterable (most flexible) | `list[T]` |
| `Set[T]` / `AbstractSet[T]` | Unique collections | `set[T]` |
| `MutableSequence[T]` | When mutation is needed | `list[T]` |
| `MutableMapping[K, V]` | When mutation is needed | `dict[K, V]` |

## Exceptions

- When your function genuinely needs list-specific features (like `.append()` mutation), use `list` for input
- When returning a view or iterator intentionally, use `Iterator` or appropriate abstract type
- For APIs where backwards compatibility matters, be consistent with existing patterns
