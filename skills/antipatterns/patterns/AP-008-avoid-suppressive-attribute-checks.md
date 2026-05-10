# AP-008: Avoid Suppressive Attribute Checks

## Category
Python/API Usage

## Description
Do not use suppressive constructs such as `getattr`, `hasattr`, or similar reflection-based fallbacks to work around unknown object structure.

## Why It's Bad
- It hides uncertainty about the real API contract
- It bypasses type checkers and makes incorrect assumptions harder to catch
- It can silently accept incompatible dependency versions
- It creates fallback behavior that may never be valid for the runtime object

## Correct Approach
- Use the documented attributes, methods, or typed interfaces directly
- Inspect local types, source code, stubs, or official documentation before using a dependency API
- If the dependency structure is unclear, report that uncertainty and wait for user approval before relying on it
- Prefer explicit adapter code or protocol types when multiple supported shapes are genuinely expected

## Examples

### Bad
```python
def extract_title(page: Page) -> str:
    metadata = getattr(page, "metadata", {})
    return getattr(metadata, "title", "")
```

```python
def submit(client: Client, payload: Payload) -> Response:
    if hasattr(client, "submit"):
        return client.submit(payload)
    return client.send(payload)
```

### Good
```python
def extract_title(page: Page) -> str:
    return page.metadata.title
```

```python
class SubmittingClient(Protocol):
    def submit(self, payload: Payload) -> Response: ...


def submit(client: SubmittingClient, payload: Payload) -> Response:
    return client.submit(payload)
```

## Exceptions

- Intentional framework integration code where reflection is the documented extension mechanism
- Serialization, plugin discovery, or compatibility layers that explicitly support multiple known shapes
- Migration code that must bridge documented API versions

When an exception applies, make the supported object shapes explicit and avoid broad silent fallbacks.
