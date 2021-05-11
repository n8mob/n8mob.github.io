---
layout: post
---
We were writing a custom `LoggerAdapter`.

Being unfamiliar with the inner-working of Python logging, we wrote some unit tests.

We learned that our logger-adapter test was failing for one team member.

The only difference we could figure out was that this team member was using Python 3.6 and I was using 3.9.

"That can't make any difference!" I thought.

And since Python is all open-sourcey, I figured I'd look at the implementations and see if they had even changed.

They had.

# LoggerAdapter in 3.6 vs 3.9

## Python 3.6: logging.LoggerAdapter
```python
def isEnabledFor(self, level):
    if self.logger.manager.disable >= level:
        return False
    return level >= self.getEffectiveLevel()
```

## Python 3.9: logging.LoggerAdapter
```python
def isEnabledFor(self, level):
    return self.logger.isEnabledFor(level)
```

It turns out, that was because our test used a `Mock()` object for the base logger ('cause that's how you unit test!)

So, `self.logger` references a **Mock**.

In 3.6, the code compares `level >= self.getEffectiveLevel()`
In 3.9 the code just returns whatever the base says (which in our case is another **Mock**)

in the `log(...)` method, the 3.9 code just asks: `if self.isEnabledFoor(level):`

...which will evaluate to True for a non-empty object

But back in 3.6 it tries to compare the log levels,

which fails because the mock returns a mock and Python doesn't know how to compare a mock to a log level (which is an int)

Oh - I looked up [the change to cpython on GitHub](https://github.com/python/cpython/commit/75f0b5dbac3376a3b36c943ec867c0daed35eb4f?branch=75f0b5dbac3376a3b36c943ec867c0daed35eb4f)
