# Changelog

## Unreleased

### Compiler

- The compiler now emits a warning when an `@internal` type appears in the
  public API of a module (e.g. as the return type or argument of a public
  function). Public type aliases are checked for their own visibility only and
  do not trigger the warning based on their aliased type.
  ([Daniele Scaratti](https://github.com/lupodevelop))

### Build tool

- `gleam publish` now refuses to publish a package if any of its modules expose
  `@internal` types in their public API. Remove the `@internal` annotation or
  update the affected signatures before publishing.
  ([Daniele Scaratti](https://github.com/lupodevelop))

### Language server

- The "extract variable" code action can now pick better names for variables in
  case branches and blocks, ignoring unrelated names of variables in other
  branches.
  ([Giacomo Cavalieri](https://github.com/giacomocavalieri))

### Formatter

### Bug fixes

- Fixed a bug where the compiler would crash when trying to read the cache for
  modules containing large constants.
  ([Surya Rose](https://github.com/GearsDatapacks))

## v1.15.1 - 2026-03-17

### Bug fixes

- Fixed a bug where `BitArray$BitArray$data` constructed a `DataView` with
  offset 0 instead of the slice's actual byte offset, causing sliced bit arrays
  to read from the wrong position in the underlying buffer on JavaScript.
  ([John Downey](https://github.com/jtdowney))
