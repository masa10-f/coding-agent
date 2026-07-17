# AP-010: Avoid Low-Value Indirection

## Category
Readability/API Design

## Description
During broad code review and refactoring, actively look for abstractions that add names, navigation, or API surface without expressing a reusable domain concept or enforcing a meaningful contract.

Treat the following as review candidates, not automatic deletions:

- A private function used once whose body only returns a literal, invokes a constructor, or performs one local validation
- A type alias or `TypeVar` that merely restates a concrete type and does not relate multiple annotations
- A public mutator or entry point with no production caller when the same behavior belongs in an existing canonical operation
- Cleanup, fallback, or default-handling code that cannot run if the class or data lifecycle invariants hold
- A generic fallback that recursively calls itself, silently accepts unsupported values, or otherwise obscures the real failure mode

## Why It's Bad
- Readers must jump through extra symbols to understand simple behavior
- Unnecessary public methods enlarge the compatibility, documentation, and test surface
- Redundant cleanup and fallback paths hide the actual state invariants
- Thin aliases and wrappers suggest reuse or meaning that does not exist
- Broken fallback paths can remain unnoticed because the indirection looks defensive

## Correct Approach
1. Define the review surface from the request. Inspect the diff for branch reviews and the relevant production modules for whole-codebase reviews.
2. Search for every reference to the symbol, including production code, tests, documentation, serialization, plugins, and subclass overrides.
3. Distinguish production callers, test-only callers, and no callers. Do not assume a library's public API is unused merely because there is no in-repository caller.
4. Read construction and mutation paths to establish the relevant invariant before removing defensive code.
5. Inline trivial logic at the canonical boundary when doing so keeps validation and behavior in one obvious place.
6. Prefer typed built-in factories and direct concrete annotations when they preserve runtime behavior and static type information.
7. Replace invalid recursive or silent fallbacks with an explicit error for unsupported inputs.
8. Update affected tests and documentation, then run behavior tests, type checking, and linting.

A review finding should state:

- The symbol or branch that adds indirection
- Evidence from callers and lifecycle invariants
- The proposed simplification
- Any public-API or compatibility risk

Do not report line count or personal style preference as sufficient evidence.

## Examples

### Bad
```python
from dataclasses import dataclass, field
from typing import TypeVar

T = TypeVar("T", bound=int)


def _empty_rules() -> dict[int, str]:
    return {}


@dataclass
class Registry:
    rules: dict[int, str] = field(default_factory=_empty_rules)
    modes: dict[int, str] = field(default_factory=dict[int, str])

    @staticmethod
    def _check_mode(mode: str) -> None:
        if mode not in {"strict", "relaxed"}:
            raise ValueError("unsupported mode")

    def register(self, key: T, value: str, *, mode: str) -> None:
        self._check_mode(mode)
        self.rules[key] = value
        self.modes[key] = mode

    def assign_mode(self, key: int, mode: str) -> None:
        self._check_mode(mode)
        self.modes[key] = mode
        # No production caller; registration is the canonical boundary.
```

### Good
```python
from dataclasses import dataclass, field


@dataclass
class Registry:
    rules: dict[int, str] = field(default_factory=dict[int, str])
    modes: dict[int, str] = field(default_factory=dict[int, str])

    def register(self, key: int, value: str, *, mode: str) -> None:
        if mode not in {"strict", "relaxed"}:
            raise ValueError("unsupported mode")
        self.rules[key] = value
        self.modes[key] = mode
```

### Bad Fallback
```python
@singledispatchmethod
def apply(self, command: Command) -> None:
    self.apply(command)
```

### Good Fallback
```python
@singledispatchmethod
def apply(self, command: Command) -> None:
    raise TypeError(f"unsupported command: {type(command).__name__}")
```

## Keep the Abstraction When
- It represents a domain concept that makes callers easier to understand
- It has multiple meaningful callers or is a documented public extension point
- A framework, serializer, dispatcher, or static type checker requires the boundary
- It isolates compatibility behavior or external input validation
- It contains independently testable logic that would obscure the caller if inlined
- Removing it would duplicate logic or weaken an explicit contract

When uncertain, prefer a concrete review note with the evidence and compatibility risk over an automatic deletion.
