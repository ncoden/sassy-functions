<h1><p align="center">SassyFunctions</p></h1>

<div align="center">
  <a href="https://github.com/ncoden/sassy-functions#-how-to-install">Install</a> | <a href="https://ncoden.github.io/sassy-functions/docs/">Documentation</a> | <a href="https://ncoden.github.io/sassy-functions/">Website</a> | <a href="https://github.com/ncoden/sassy-functions/releases">Releases</a>
</div>

<div align="center">
  🎉 The little toolbox to use functions across all Sass versions
</div>

<br>

## 🤔 Why?

In order to improve modular namespacing, Sass 4 will only accept first-class functions as argument for `call()` so functions will be called in their own context. This allow developers to make their Sass packages more modular while still being able to call functions given by the user. As a first step, Sass 3.5 added `get-function()` to get a first-class function from its name and throw a warning if a function name string is passed to `call()`.

We are now encouraged to use `get-function()`, but this would break our packages for older Sass versions. SassyFunctions is there to allow you to process first-hand functions and function name strings the same way and continue to support all Sass versions.

[![Build Status](https://travis-ci.org/ncoden/sassy-functions.svg?branch=develop)](https://travis-ci.org/ncoden/sassy-functions)
[![devDependencies Status](https://david-dm.org/ncoden/sassy-functions/dev-status.svg)](https://david-dm.org/ncoden/sassy-functions?type=dev)

<br>

## 👷 How to install

```sh
$ npm i -D sassy-functions
```

Then in Sass:
```scss
@import '/path/to/node_modules/sassy-functions/scss/sassy-functions';
```

Or with [Eyeglass](https://github.com/sass-eyeglass/eyeglass#writing-an-eyeglass-module)
```scss
@import 'sassy-functions';
```

<br>

## 👩‍💻 How to use

### Basic examples

```scss
// Safely use any function reference or name coming from anywhere...
@function map($list, $func) {
  $newlist: ();
  @each $v in $list {
    $newlist: append($newlist, sf-call($func, $v));
  }
  @return $newlist;
}

// ...Or safely pass your own function names to anywhere!
$my-list: ('hello', 'word');
$uppercased-list: map($my-list, sf-get-function(to-upper-case));
```

### Functions

* **`sf-is-function($value)`**
  Return if a given value is a function name or reference.

* **`sf-is-callable($value)`**
  Return if a given value can be called.

* **`sf-assert-function($value)`**
  Check if a given value is a function name or reference and throw an error otherwise.

* **`sf-assert-callable($value)`**
  Check if a given value can be called and throw the appropriate error otherwise.

* **`sf-get-function($func)`**
  Return a reference to the given function or a function name string so it is callable in the current Sass version. For Sass < 3.5, return the passed argument. For Sass >= 3.5, return a function reference if a function name string was passed.

* **`sf-call($func, $args...)`**
  Polyfill for the `call` function supporting both function names and references.

[See the full API documentation](https://ncoden.github.io/sassy-functions/docs)

<br>

## 👩‍🔬 Testing

You can install SassyFunctions locally and test it with:
```sh
# Clone the repo
git clone git@github.com:ncoden/sassy-functions.git
cd sassy-functions

# Install dependencies
npm install

# Run tests
npm test
```

<br>

---

<br>

<div align="center">
  Made with ❤️  in Paris

  Copyright © 2018, [Nicolas Coden](https://github.com/ncoden).
  Released under the [MIT license](https://github.com/ncoden/sassy-functions/blob/master/LICENSE).
</div>
