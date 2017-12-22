# type_spec - Pre/Post conditions for Python functions

This is a python module that type checks for Python function arguments
and return values.

## Example Usage

A function that takes built-in types:

```python
from type_spec import typeSpec

@typeSpec(int, int, int)
def add(a, b):
  return a + b
```

A function that takes any of a number of built in types with certain constraints:

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

## Usage Details

To specify a pre/post condition for your function you use the `typeSpec`
decorator. The signature is:

```
typeSpec(arg_1_type, ..., arg_n_type, return_type)
```

The arguments/types provided to typeSpec can be any of the following:

* A built-in type such as `int`, `float`, `str`, `bool`, `list`, `dict`, `set` etc.
* A class, i.e. `MyClass`
* A function/callable that takes a value as argument and returns `None` if the value has a valid type and an error message (string) otherwise.
* A `dict` instance that specifies that a valid value must be a dictionary with a certain structure, i.e. `{'name': str, 'enabled': bool}`
* A `list` instance that specifies that a valid value must be a list with items of a certain
type, i.e. `[str]`.
* A predicate function that returns True or False, i.e. `lambda n: n > 0`
* An example value/instance, i.e. `None`, `"2017-01-01"`. This means the value needs to be an instance of the same type as the example value.
