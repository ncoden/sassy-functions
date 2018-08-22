# Changelog

## 0.3.0 (22 August 2018)

This release add settings to customize the error messages and improve the API documentation.

* **`$sf-error-prefix`**  
  Prefix for all the error messages

* **`$sf-error-function-invalid`**  
  Error message for when a function name or reference is expected but an other value is received.

* **`$sf-error-function-reference-invalid`**  
  Error message for when a first-class function reference is expected but an other value is received.

* **`$sf-error-function-not-found`**  
  Error message for when a function name cannot be found and the `get-function` function is not availaible (Sass < 3.5).

* **`$sf-error-function-not-found-get-function`**  
  Error message for when a function name cannot be found and the `get-function` function is availaible (Sass >= 3.5).

### All changes
* 🚀 91d8af1 - Add settings to customize error messages
* 💻 334b3d5 - Add helpers to handle custom error messages
* 📖 06ddd1b - Fix links in footer of the README.md
* 📖 5104966 - Move the API doc to its own section in README.md
* 📖 171081e - Add full usage documentation to README.md

## 0.2.0 (11 Jun 2018)

This release add unit tests and improve the SassyFunction documentation.

### All changes
* 💻 9d5fed7 - Update Lockfiles
* 📖 819e472 - Add testing section in README.md
* 🚨 424e6c8 - Add tests for testable functions
* 📖 db70bfe - Fix typos in README.md
* 🐛 54f04e1 - Fix Yarn node-sass instrallation in Travis tests
* 📖 9153753 - Use original vendor badges in README.md
* 📖 cc9b98a - Improve README.md license footer
* 📖 0268359 - Add Travis and David badges to README.md
* 💻 6db0eb1 - Run tests with Travis
* 💻 348a59c - Add Yarn lockfile
* 💻 546b868 - Add setup for Sass unit tests
* 📖 5a1019d - Fix menu links in README.md
* 📖 6c72b03 - Add functions list to README.md
* 📖 55637c2 - Improve README.md header design and add menu
* 💻 7608d7f - Set up SassDoc configuration

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
