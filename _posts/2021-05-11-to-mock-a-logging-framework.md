---
layout: post
---

# Python LoggerAdapter in 3.6 vs 3.9

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

so - our logger-adapter test was failing because it used a `Mock()` object for the base logger under the ('cause that's how you unit test!)

so, `self.logger` is a **Mock**

In 3.6, the code compares `level >= self....`
In 3.9 the code just returns whatever the base says (which in our case is another **Mock**)

in the `log(...)` method, the 3.9 code just asks: `if self.isEnabledFoor(level):`

...which will evaluate to True for a non-empty object

But back in 3.6 it tries to compare the log levels,

which fails because the mock returns a mock and Python doesn't know how to compare a mock to a log level (which is an int)

