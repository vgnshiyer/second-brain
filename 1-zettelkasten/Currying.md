Created on 2024-08-02_11-19-51

## 📔 Notes

Curry police 🚨

TIL:

**Currying:**

Function that takes multiple arguments is partially initiated with a partial set of arguments fixed. This allows partial application of a function with some args fixed and return a new function which takes the remaining arguments.

```python
from functions import partial

def add(a, b):
    return a + b

add_5 = partial(add, 5)

print(add_5(10))  # 15

```

## 🔗 Links

- [[Tech]]
- [[Road to principal engineer]]
