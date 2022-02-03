---
title: A nice way to catch multiple exceptions in Python
updated: 2022-02-03 15:40
---

Recently I had a need to generically handle exceptions, so I built a function to do the trick.

```
def check_throw_exception(
    func: Any,
    *args: Any,
    to_be_catched: Type[Exception],
    to_be_throw: Type[<some_custom_exception_or_not>],
    **kwargs: Any
) -> Any:
    try:
        return func(*args, **kwargs)
    except to_be_catched as err:
        <logging_the_exception>
        raise to_be_throw()
```

The check_throw_exception function wraps a function call inside of try/except clause, catches the defined exception (if occurred) and throw another defined exception. So far, so good.

But, I had to catch more than one exception, because the function call wrapped by the check_throw_exception function could to be
thrown more than one exception and the handler only catches one exception... So, how to do it avoiding to write multiples except
clauses? Here we go.

```
def check_throw_exception(
    func: Any,
    *args: Any,
    to_be_catched: Union[Tuple[Type[Exception]], Type[Exception]],
    to_be_throw: Type[<some_custom_exception_or_not>],
    **kwargs: Any
) -> Any:
    try:
        return func(*args, **kwargs)
    except to_be_catched as err:
        <logging_the_exception>
        raise to_be_throw()
```

Python supports multiple exceptions in one except clause ([docs](https://docs.python.org/3/tutorial/errors.html#handling-exceptions)) when the exceptions are defined inside of a tuple, then I changed the param to_be_catched to receive a tuple of exceptions.
