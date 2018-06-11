# Changelog

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
