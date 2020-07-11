runtime-assert
==============

> Runtime asserts for ZZ

## Installation

Add this to your `zz.toml` file:

```toml
[dependencies]
runtime_assert = "*"

[repos]
runtime_assert = "git://github.com/zzmodules/runtime-assert"
```

## Usage

```c++
using runtime_assert
```

## API

### `runtime_assert::assert(assertion)`

Makes a runtime assertion. Upon failure, this function will
call [`abort_signal::abort()`][abort_signal].

```c++
using runtime_assert::{ assert }

fn main() -> int {
  assert(false); // will abort here
  return 0;
}
```

#### Catching assertion errors

An abort signal callback function handler can be set to catch errors.

```c++
using abort_signal::{ set_abort_callback }
using log
using runtime_assert::{ assert }

static usize mut aborts = 0;

fn onabort() {
  aborts++;
}

fn main() -> int {
  set_abort_callback(onabort);

  assert(false);
  assert(false);
  assert(false);

  log::info("fails = %lu", aborts); // 3
  return 0;
}
```

## See Also

* [abort-signal][abort_signal]

## License

MIT

[abort_signal]: https://github.com/zzmodules/abort-signal#api
