# Changelog

## 0.1.0 (6 Jun 2018)

First release of SassyFunctions with the following functions:

* **`sf-is-function($value)`**
  Return if a given value is a function name or reference.

* **`sf-is-callable($value)`**
  Return if a given value can be called.

* **`sf-assert-function($value)`**
  Check if a given value is a function name or reference and throw an error otherwise.

* **`sf-assert-callable($value)`**
  Check if a given value can be called and throw the appropriate error otherwise.

* **`sf-get-function($func)`**
  Return a reference to the given function or function name string compatible with the current Sass version. For Sass < 3.5, return the passed argument. For Sass >= 3.5, return a function reference if a function name string was passed.

* **`sf-call($func, $args...)`**
  Polyfill for the `call` function supporting both function names and references.
