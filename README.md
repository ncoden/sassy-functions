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

[![build status](https://img.shields.io/travis/ncoden/sassy-functions.svg)](https://travis-ci.org/ncoden/sassy-functions)
[![dev dependencies](https://img.shields.io/david/dev/ncoden/sassy-functions.svg)](https://david-dm.org/ncoden/sassy-functions?type=dev)
[![npm](https://img.shields.io/npm/v/:sassy-functions.svg)](https://www.npmjs.com/package/sassy-functions)

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

**Package maintainers**, safely use any function reference or name coming from anywhere!

```scss
// Let's say you provide a "map-on-my-list" function to iterate with given function on a list...
@function map-on-my-list($list, $func) {
  $newlist: ();

  @each $v in $list {
    $newlist: append($newlist, sf-call($func, $v));
  }
  
  @return $newlist;
}
```

**Package users**, safely pass your own function names to anywhere!

```scss
// Let's say you have a "to-upper-case" function and want to map a list on it...
$my-list: ('hello', 'world');
$uppercased-list: map-on-my-list($my-list, sf-get-function(to-upper-case));
```

✨ There is more! See the [API](#api) to discover all the functions of the SassyFunctions toolbox.

<br>

## 📘 API

* **`sf-is-function($value)`**

  Return if a given value is a function name or reference.

  For example it returns `true` for:
  ```scss
  // A native Sass function name string
  $res: sf-is-function(rgba);
  // Your own function name string
  $res: sf-is-function('my-function');
  // An inexistant function name (any string can be a function name)
  $res: sf-is-function('xqxqqxhnxqh');
  // A first-class function (in Sass > 3.5)
  $res: sf-is-function(get-function(rgba));
  ```

  And it will returns `false` for:
  ```scss
  // Any value that is not a string or a first-class function
  $res: sf-is-function(0);
  $res: sf-is-function(());
  ```
  <br>

* **`sf-is-callable($value)`**

  Return if a given value can be called.

  For example it returns `true` for:
  ```scss
  // A native Sass function name string
  $res: sf-is-function(rgba);
  // Your own function name string
  $res: sf-is-function('my-function');
  // A first-class function (in Sass > 3.5)
  $res: sf-is-function(get-function(rgba));
  ```

  And it will returns `false` for:
  ```scss
  // Any value that is not a string or a first-class function
  $res: sf-is-function(0);
  $res: sf-is-function(());
  // A function name that cannot be found
  $res: sf-is-function('xqxqqxhnxqh');
  ```
  <br>

* **`sf-assert-function($value)`**

  Check if a given value is a function name or reference and throw an error otherwise. See `sf-is-function` for informations on the expected value.

  You can use it to check for your user arguments like:
  ```scss
  @function example($callback) {
    $_: sf-assert-function($callback);

    // ...your code with $callback secured..
  }
  ```
  <br>

* **`sf-assert-callable($value)`**

  Check if a given value can be called and throw the appropriate error otherwise. See `sf-is-callable` for informations on the expected value.

  You can use it to check for your user arguments like:
  ```scss
  @function example($callback) {
    $_: sf-assert-callable($callback);

    // ...your code with $callback secured..
    $res: call($callback);
  }
  ```

  If `$value` is not a function, it will throw an error with the appropriate message according to the Sass version used, with migration guidelines if relevant.
  <br><br>

* **`sf-get-function($func)`**

  Return a reference to the given function or a function name string so it is callable in the current Sass version. For Sass < 3.5, return the passed argument. For Sass >= 3.5, return a function reference if a function name string was passed.

  For example, use `sf-get-function` to get a function you can call no matter which Sass version is running.
  ```scss
  @function example($callback) {
    $safe-function: sf-get-function($callback);

    // ...your code with $safe-function secured..
  }
  ```
  <br>

* **`sf-call($func, $args...)`**

  Polyfill for the `call` function supporting both function names and references. Calls the given function/name `$func` with all the following arguments `$args...`). If the function cannot be called, throw the appropriate error depending on the user environement.

  For example, use `sf-call` to call a user-provided callback no matter which Sass version is running.
  ```scss
  @function example($callback) {
    // ...do your stuff...
    $value: random();

    // ...then call the callback.
    $res: sf-call($callback, $value);
  }
  ```
  <br>

  <div align="center">
    <hr>
    <a href="https://ncoden.github.io/sassy-functions/docs">📖 See the full API documentation</a>
    <hr>
  </div>

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

  Copyright © 2018, <a href="https://github.com/ncoden">Nicolas Coden</a>.
  Released under the <a href="https://github.com/ncoden/sassy-functions/blob/master/LICENSE">MIT license</a>.
</div>
