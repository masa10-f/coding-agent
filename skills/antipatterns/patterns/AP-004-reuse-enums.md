# AP-004: Reuse Existing Enums

## Category
Code Reuse

## Description
When the codebase already defines an enum for a particular purpose, reuse that existing enum instead of creating a new one with similar or identical values.

## Why It's Bad
- Duplicate enums create confusion about which one to use
- Changes to one enum won't be reflected in duplicates
- Type checking becomes inconsistent across the codebase
- It violates the DRY (Don't Repeat Yourself) principle
- Comparison between different enum types will fail even if values match

## Correct Approach
1. Search the codebase for existing enums before creating new ones
2. Import and use the existing enum from its original location
3. If the existing enum needs additional values, extend it properly or discuss with the team
4. Document where the canonical enum definition lives

## Examples

### Bad
```python
# file: services/payment.py
from enum import Enum

class PaymentStatus(Enum):  # Duplicating existing enum!
    PENDING = "pending"
    COMPLETED = "completed"
    FAILED = "failed"

def process_payment(status: PaymentStatus) -> None:
    pass
```

```python
# file: models/order.py (existing enum)
from enum import Enum

class OrderPaymentStatus(Enum):
    PENDING = "pending"
    COMPLETED = "completed"
    FAILED = "failed"
```

### Good
```python
# file: services/payment.py
from models.order import OrderPaymentStatus

def process_payment(status: OrderPaymentStatus) -> None:
    pass
```

## How to Find Existing Enums

Before creating a new enum, search the codebase:

```bash
# Search for enum definitions
grep -r "class.*Enum" --include="*.py" .
grep -r "class.*StrEnum" --include="*.py" .

# Search for specific enum values you need
grep -r "PENDING\|COMPLETED\|FAILED" --include="*.py" .
```
