# PYTHON VARIABLE ANNOTATIONS AND DUCK TYPING {#py-vars}

---

## Type Annotations

Introduced in Python 3.5 through [PEP 484](https://peps.python.org/pep-0484) type annotations are a way of specifying the expected types of variables, function parameters, and return values. They are primarily used for documentation and static analysis purposes and are not enforced by the Python interpreter itself.

### Syntax of Type Annotations

Type annotations are specified using the `:` syntax following the variable or function parameter name and using `->` for return values for functions.

Variable Types:
: ``
x: int = 5
y: int # no need to initialize a variable to annotate it
``

Function Signatures:
: ``
def add(x: int, y: int) -> int:
    return x + y
``

## Usage

### Acceptable Type Hints

- Type hints may include built-in classes, abstract base classes, `types` from the types module, and user-defined classes.

```python
from typing import List, Tuple

def process_data(data: List[int]) -> Tuple[int, float]:
    # Process data...
    return total, average

```

### Type Aliases

- Type aliases provide convenient names for complex types.
They allow defining shorthand names for complex types to improve code readability.
They are defined using simple variable assignments.

```python
from typing import TypeVar, Iterable, Tuple

T = TypeVar('T', int, float, complex)
Vector = Iterable[Tuple[T, T]]

def inproduct(v: Vector[T]) -> T:
    return sum(x*y for x, y in v)
```

### Callable

- Annotate callback functions with specific signatures.
`Callable` is followed by the call signature of the function it accepts.

```python
from typing import Callable

def feeder(get_next_item: Callable[[], str]) -> None:
    # Function body

def async_query(on_success: Callable[[int], None],
                on_error: Callable[[int, Exception], None]) -> None:
    # Function body

```

### Generics

- Define generic functions or classes to work with any type.
They are declared using `TypeVar`

```python
from typing import TypeVar, List

T = TypeVar('T')

def first_item(items: List[T]) -> T:
    return items[0]

```

#### TypeVar with Constraints

- Constrain type variables to a fixed set of possible types.

```python
from typing import TypeVar, List, Text

AnyStr = TypeVar('AnyStr', Text, bytes)

def concat(x: AnyStr, y: AnyStr) -> AnyStr:
    return x + y
```

#### Type Annotations with TypeVar

- Use TypeVar to declare type variables within generic functions or classes.

```python
from typing import TypeVar, Generator

T = TypeVar('T')

def process_data(data: Generator[T, None, None]) -> None:
    for item in data:
        # Process item...
```

#### Scoping Rules for Type Variables

- Type variables follow normal name resolution rules but have specific rules within generic functions or classes.

```python
from typing import TypeVar, List

T = TypeVar('T')

def process_data(items: List[T]) -> None:
    for item in items:
        # Process item...
```

#### Using Type[] to Access Class Objects

- Type[] allows referring to class objects, especially useful for creating instances of subclasses.

```python
from typing import Type, TypeVar

T = TypeVar('T')

def create_instance(cls: Type[T]) -> T:
    return cls()
```

### Union Types

- Union types allow specifying that a variable can accept values of multiple types.
They are represented as Union[T1, T2, ...].

```python
from typing import Union

def process_value(value: Union[int, float, str]) -> None:
    # Process value...
```

## Duck Typing

Duck typing is a style of dynamic typing in which an object's methods and properties determine its compatibility with other objects rather than its inheritance hierarchy or explicit type.
In duck typing, the focus is on what an object can do, rather than what type it is. That is, the type or the class of an object is less important than the methods it defines. If an object implements certain methods, it can be used interchangeably with any other object that implements the same methods, regardless of their class.

*For instance, if an object has a quack() method and a walk() method, it can be treated as a duck, regardless of its actual type.*[^1]

[MyPy CheatSheet](https://mypy.readthedocs.io/en/latest/cheat_sheet_py3.html)

[^1]: *If it looks like a duck and quacks like a duck, it must be a duck.*
