# Changelog

## Unreleased

### Compiler

- The compiler now warns when a public function, constructor, or constant
  exposes an `@internal` type — for example as a return type or argument.
  This helps catch accidental API surface leaks where a type has no
  documentation and callers cannot refer to it by name.
  Using `pub type Alias = InternalType` is a safe escape hatch: the alias is
  public, so using it in a public signature does not trigger the warning.
  ([Daniele Scaratti](https://github.com/lupodevelop))

### Build tool

- `gleam publish` now refuses to publish a package whose public API exposes
  an `@internal` type directly. If you see this error, either remove the
  `@internal` annotation from the type, introduce a public alias, or update
  the affected signatures to use a non-internal type.
  > **Note:** this release changes the internal format used to cache compiled
  > module metadata. After upgrading, run `gleam clean` once in each of your
  > projects to avoid stale-cache errors
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
