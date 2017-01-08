---
layout: post
title: Python 3.6.0
---

## This just in, Python 3.6.0 is out now!

What's new in this update?

- **New syntax features:**

	- PEP 498, formatted string literals.
	- PEP 515, underscores in numeric literals.
	- PEP 526, syntax for variable annotations.
	- PEP 525, asynchronous generators.
	- PEP 530: asynchronous comprehensions.

- **New library modules:**

	- `secrets:`PEP 506 – Adding A Secrets Module To The Standard Library.

- **Security improvements:**

	- The new `secrets` module has been added to simplify the generation of cryptographically strong pseudo-random numbers suitable for managing secrets such as account authentication, tokens, and similar.
	- On Linux, `os.urandom()` now blocks until the system urandom entropy pool is initialized to increase the security. See the PEP 524 for the rationale.
	- The `hashlib` and `ssl` modules now support OpenSSL 1.1.0.
	- The default settings and feature set of the `ssl` module have been improved.
	- The `hashlib` module received support for the BLAKE2, SHA-3 and SHAKE hash algorithms and the `scrypt()` key derivation function.

## Syntax

**PEP 498: Formatted string literals**

PEP 498 introduces a new kind of string literals: f-strings, or formatted string literals.
Formatted string literals are prefixed with 'f' and are similar to the format strings accepted by `str.format()`. They contain replacement fields surrounded by curly braces. The replacement fields are expressions, which are evaluated at run time, and then formatted using the `format()` protocol:

```Python
>>> name = "Fred"
>>> f"He said his name is {name}."
'He said his name is Fred.'
>>> width = 10
>>> precision = 4
>>> value = decimal.Decimal("12.34567")
>>> f"result: {value:{width}.{precision}}"  # nested fields
'result:      12.35'
```


**PEP 515: Underscores in Numeric Literals**

PEP 515 adds the ability to use underscores in numeric literals for improved readability. For example:

```Python
>>>
>>> 1_000_000_000_000_000
1000000000000000
>>> 0x_FF_FF_FF_FF
4294967295
```

Single underscores are allowed between digits and after any base specifier. Leading, trailing, or multiple underscores in a row are not allowed.

The string formatting language also now has support for the '_' option to signal the use of an underscore for a thousands separator for floating point presentation types and for integer presentation type 'd'. For integer presentation types 'b', 'o', 'x', and 'X', underscores will be inserted every 4 digits:

```Python
>>>
>>> '{:_}'.format(1000000)
'1_000_000'
>>> '{:_x}'.format(0xFFFFFFFF)
'ffff_ffff'
```


**PEP 526: Syntax for variable annotations**

PEP 484 introduced the standard for type annotations of function parameters, a.k.a. type hints. This PEP adds syntax to Python for annotating the types of variables including class variables and instance variables:

```Python
primes: List[int] = []

captain: str  # Note: no initial value!

class Starship:
    stats: Dict[str, int] = {}
```

Just as for function annotations, the Python interpreter does not attach any particular meaning to variable annotations and only stores them in the `__annotations__` attribute of a class or module.

In contrast to variable declarations in statically typed languages, the goal of annotation syntax is to provide an easy way to specify structured type metadata for third party tools and libraries via the abstract syntax tree and the `__annotations__` attribute.


**PEP 525: Asynchronous Generators**

PEP 492 introduced support for native coroutines and `async` / `await` syntax to Python 3.5. A notable limitation of the Python 3.5 implementation is that it was not possible to use await and yield in the same function body. In Python 3.6 this restriction has been lifted, making it possible to define asynchronous generators:

```Python
async def ticker(delay, to):
    """Yield numbers from 0 to *to* every *delay* seconds."""
    for i in range(to):
        yield i
        await asyncio.sleep(delay)
```


**PEP 530: Asynchronous Comprehensions**

PEP 530 adds support for using async for in list, set, dict comprehensions and generator expressions:

```Python
result = [i async for i in aiter() if i % 2]
```

Additionally, await expressions are supported in all kinds of comprehensions:

`result = [await fun() for fun in funcs if await condition()]`
