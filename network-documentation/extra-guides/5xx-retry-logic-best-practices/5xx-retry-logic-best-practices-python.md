---
description: Review best practices to deal with 5XX errors in Python
---

# 5XX Retry Logic Best Practices - Python

## Method 1

```python
import requests
from requests.adapters import HTTPAdapter
from requests.packages.urllib3.util.retry import Retry


def requests_retry_session(
    retries=3,
    backoff_factor=0.3,
    status_forcelist=(500, 502, 504),
    session=None,
):
    session = session or requests.Session()
    retry = Retry(
        total=retries,
        read=retries,
        connect=retries,
        backoff_factor=backoff_factor,
        status_forcelist=status_forcelist,
    )
    adapter = HTTPAdapter(max_retries=retry)
    session.mount('http://', adapter)
    session.mount('https://', adapter)
    return session
```

### Example

```python
response = requests_retry_session().get('https://www.peterbe.com/')
print(response.status_code)

s = requests.Session()
s.auth = ('user', 'pass')
s.headers.update({'x-test': 'true'})
response = requests_retry_session(session=s).get(
    'https://www.peterbe.com'
)
```

Get more details and examples [HERE](https://www.peterbe.com/plog/best-practice-with-retries-with-requests).

## **Method 2**

Using pip install retry.

**Features**

* No external dependency \(stdlib only\).
* \(Optionally\) Preserve function signatures \(pip install decorator\).
* Original traceback, easy to debug.

**Installation**

```python
$ pip install retry
```

**API, Retry Decorator**

```python
def retry(exceptions=Exception, tries=-1, delay=0, max_delay=None, backoff=1, jitter=0, logger=logging_logger):
    """Return a retry decorator.

    :param exceptions: an exception or a tuple of exceptions to catch. default: Exception.
    :param tries: the maximum number of attempts. default: -1 (infinite).
    :param delay: initial delay between attempts. default: 0.
    :param max_delay: the maximum value of delay. default: None (no limit).
    :param backoff: multiplier applied to delay between attempts. default: 1 (no backoff).
    :param jitter: extra seconds added to delay between attempts. default: 0.
                   fixed if a number, random if a range tuple (min, max)
    :param logger: logger.warning(fmt, error, delay) will be called on failed attempts.
                   default: retry.logging_logger. if None, logging is disabled.
    """
```

Various types of retry logic can be achieved by combining different arguments. See examples [HERE](https://pypi.org/project/retry/).

## Method 3

Using a Retry Decorator

```python
from functools import wraps
import time
import logging
import random

logger = logging.getLogger(__name__)


def retry(exceptions, total_tries=4, initial_wait=0.5, backoff_factor=2, logger=None):
    """
    calling the decorated function applying an exponential backoff.
    Args:
        exceptions: Exeption(s) that trigger a retry, can be a tuble
        total_tries: Total tries
        initial_wait: Time to first retry
        backoff_factor: Backoff multiplier (e.g. value of 2 will double the delay each retry).
        logger: logger to be used, if none specified print
    """
    def retry_decorator(f):
        @wraps(f)
        def func_with_retries(*args, **kwargs):
            _tries, _delay = total_tries + 1, initial_wait
            while _tries > 1:
                try:
                    log(f'{total_tries + 2 - _tries}. try:', logger)
                    return f(*args, **kwargs)
                except exceptions as e:
                    _tries -= 1
                    print_args = args if args else 'no args'
                    if _tries == 1:
                        msg = str(f'Function: {f.__name__}\n'
                                  f'Failed despite best efforts after {total_tries} tries.\n'
                                  f'args: {print_args}, kwargs: {kwargs}')
                        log(msg, logger)
                        raise
                    msg = str(f'Function: {f.__name__}\n'
                              f'Exception: {e}\n'
                              f'Retrying in {_delay} seconds!, args: {print_args}, kwargs: {kwargs}\n')
                    log(msg, logger)
                    time.sleep(_delay)
                    _delay *= backoff_factor

        return func_with_retries
    return retry_decorator


def log(msg, logger=None):
    if logger:
        logger.warning(msg)
    else:
        print(msg)


def test_func(*args, **kwargs):
    rnd = random.random()
    if rnd < .2:
        raise ConnectionAbortedError('Connection was aborted :(')
    elif rnd < .4:
        raise ConnectionRefusedError('Connection was refused :/')
    elif rnd < .8:
        raise ConnectionResetError('Guess the connection was reset')
    else:
        return 'Yay!!'


if __name__ == '__main__':
    # wrapper = retry((ConnectionAbortedError), tries=3, delay=.2, backoff=1, logger=logger)
    # wrapped_test_func = wrapper(test_func)
    # print(wrapped_test_func('hi', 'bye', hi='ciao'))

    wrapper_all_exceptions = retry(Exception, total_tries=2, logger=logger)
    wrapped_test_func = wrapper_all_exceptions(test_func)
    print(wrapped_test_func('hi', 'bye', hi='ciao'))
```

Get the code [HERE](https://gist.github.com/FBosler/be10229aba491a8c912e3a1543bbc74e).

Get more details [HERE](https://towardsdatascience.com/are-you-using-python-with-apis-learn-how-to-use-a-retry-decorator-27b6734c3e6).

