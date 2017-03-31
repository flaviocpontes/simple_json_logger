# Simple Json Logger

A simple, thin layer, drop-in replacement of python built-in Logger from
the `logging` module, that grants to always log valid json output.

## Installation

`pip install simple_json_logger`

## Testing

`python -m unittest discover`

## Usage

### Hello world

``` python

from simple_json_logger import JsonLogger


def foo():
    logger = JsonLogger()

    logger.info("Hello world!")

foo()
>>> {"msg": "Hello world!", "logged_at": "2017-03-31T02:10:16.786569", "line_number": 6, "function": "foo", "level": 20, "path": "/Volumes/partition2/Users/diogo/PycharmProjects/simple_json_logger/bla.py"}
```


### stdin / stderr

By default, JsonLogger handle `debug` and `info` as `stdout` and
 `warning`, `critical`, `exception` and `error` as `stderr`.

``` python

from simple_json_logger import JsonLogger


def foo():
    logger = JsonLogger()

    logger.debug("I'm a json in stdout !")
    logger.info("I'm a json in stdout !")

    logger.warning("I'm a json in stderr !")
    logger.error("Wow i'm json in stderr !")
    logger.critical("Wow i'm json in stderr !")

foo()
>>> {"msg": "I'm a json in stdout !", "logged_at": "2017-03-31T02:37:46.616014", "line_number": 7, "function": "foo", "level": 10, "path": "/Volumes/partition2/Users/diogo/PycharmProjects/simple_json_logger/bla.py"}
>>> {"msg": "I'm a json in stdout !", "logged_at": "2017-03-31T02:37:46.616145", "line_number": 8, "function": "foo", "level": 20, "path": "/Volumes/partition2/Users/diogo/PycharmProjects/simple_json_logger/bla.py"}
>>> {"msg": "Wow i'm json in stderr !", "logged_at": "2017-03-31T02:37:46.616225", "line_number": 9, "function": "foo", "level": 30, "path": "/Volumes/partition2/Users/diogo/PycharmProjects/simple_json_logger/bla.py"}
>>> {"msg": "Wow i'm json in stderr !", "logged_at": "2017-03-31T02:37:46.616298", "line_number": 11, "function": "foo", "level": 40, "path": "/Volumes/partition2/Users/diogo/PycharmProjects/simple_json_logger/bla.py"}
>>> {"msg": "Wow i'm json in stderr !", "logged_at": "2017-03-31T02:37:46.616369", "line_number": 12, "function": "foo", "level": 50, "path": "/Volumes/partition2/Users/diogo/PycharmProjects/simple_json_logger/bla.py"}
```

 You may override that behavior by passing your own `stream` handler.

 ``` python

 import sys
 from simple_json_logger import JsonLogger


 logger = JsonLogger(stream=sys.stdout)

 logger.error("I'll always log to stdout!!!")
 >>> {"msg": "I'll always log to stdout!!!", "logged_at": "2017-03-31T02:43:44.883072", "line_number": 5, "function": "<module>", "level": 40, "path": "/Volumes/partition2/Users/diogo/PycharmProjects/simple_json_logger/bla.py"}

 ```

## Depencencies

Has none