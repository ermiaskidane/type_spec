# type_spec - Pre/Post conditions for Python functions

This is a python module that type checks for Python function arguments
and return values.

## Example Usage

```python
from type_spec import typeSpec, AllOf, AnyOf, type_check

def Number(v):
    return type_check(v, AnyOf(int, float))

def GreaterThanZero(v):
    if v <= 0:
        return 'must be greater than zero'

@typeSpec(Number, AllOf(Number, GreaterThanZero), Number)
def div(a, b):
    return a / b
```
