# Context Managers

- Interesting uses
    - Cleanup/delete an object in a structured way
    - `__del__` is ONLY called on an object when `del()` is called on it AND
      the reference count is 0
        - So, you only get to run anything when the reference count is zero and
          you can never actually guarantee that will happen in the case of
          circular references.


# Generator

- Several ways to think of it:
    1. Just a function with a stack frame that doesn't get cleaned up until the
       end of the application
    2. Just an object/function that has a `next()` method
    3. Function with 1 property that can hold state and return


```python
>>> def func():
...  return
... 
>>> def gen():
...  yield
... 
>>> from dis import dis
RuntimeError: no last traceback to disassemble
>>> dis(func)
  2           0 LOAD_CONST               0 (None)
              3 RETURN_VALUE        
>>> dis(gen)
  2           0 LOAD_CONST               0 (None)
              3 YIELD_VALUE         
              4 POP_TOP             
              5 LOAD_CONST               0 (None)
              8 RETURN_VALUE        
```


- `yield` is not a statement, it's really an expression
- Generators are now coroutines so you can pass values back into them
- Look for places where you are just maintaining local state and extract into a
  generator
- Yield unbounded streams of data and allow callers to loop over the stream so
  they can take out what they want and still only use constant memory usage

```python
def func():
    total = 0
    for x in xrange(1, 1001):
        if x % 1 == 0:
            total += x

    return total
```

- Tracking total is just local state


#### Misc

- built-in `any()` method to look through an iterable for a truth value

```python
>>> any((x for x in [0, 1, 2, 3]))
True
>>> any((x for x in [0]))
False
```

- `seq` shell command to generate a sequence of values to `stdout`
- What makes an interator/generator/etc.?
    - [http://docs.python.org/library/collections.html#collections-abstract-base-classes](http://docs.python.org/library/collections.html#collections-abstract-base-classes)
