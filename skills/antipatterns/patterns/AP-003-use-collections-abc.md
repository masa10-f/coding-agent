# AP-003: Use collections.abc for Generic Types

## Category
Python/Typing

## Description
For generic types like `Sequence`, `Mapping`, `Iterable`, `Iterator`, `Callable`, etc., import them from `collections.abc` instead of `typing`.

## Why It's Bad
- Importing generic types from `typing` is deprecated since Python 3.9
- The `typing` module versions are maintained only for backward compatibility
- Using `typing` versions creates inconsistency in modern codebases
- Future Python versions may remove these from `typing`

## Correct Approach
Import abstract base classes from `collections.abc`:
- `Sequence`, `MutableSequence`
- `Mapping`, `MutableMapping`
- `Set`, `MutableSet`
- `Iterable`, `Iterator`
- `Callable`
- `Collection`
- `Container`
- etc.

## Examples

### Bad
```python
from typing import Sequence, Mapping, Iterable, Callable, Iterator

def process_items(items: Sequence[str]) -> Mapping[str, int]:
    pass

def apply_func(func: Callable[[int], str], items: Iterable[int]) -> Iterator[str]:
    pass
```

### Good
```python
from collections.abc import Sequence, Mapping, Iterable, Callable, Iterator

def process_items(items: Sequence[str]) -> Mapping[str, int]:
    pass

def apply_func(func: Callable[[int], str], items: Iterable[int]) -> Iterator[str]:
    pass
```

## Note
For concrete types like `list`, `dict`, `set`, `tuple`, you can use the built-in types directly (since Python 3.9):

```python
# Good - using built-in types directly
def process(items: list[str]) -> dict[str, int]:
    pass
```
