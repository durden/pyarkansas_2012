# What is Python and why is it cool?

## Jeff Rush

- Decimal module in Python 3 is literally 100x faster than Python 2
- Never use floating point numbers for currency, use Decimal
    - Round off errors, etc.

- Use buffer protocol to see actual locations/size in memory, etc.
    - [Buffer protocol](http://python.readthedocs.org/en/v2.7.2/c-api/buffer.html#bufferobjects)
    - [Buffer protocol Python 3](http://docs.python.org/dev/c-api/buffer.html)

- Object is 'subscriptable' if it implements `__getitem__`
