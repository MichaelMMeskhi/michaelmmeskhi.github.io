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

PEP 498: Formatted string literals

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

