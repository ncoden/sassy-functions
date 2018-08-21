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
$my-list: ('hello', 'world');
$uppercased-list: map($my-list, sf-get-function(to-upper-case));
```

### Functions

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

* **`sf-assert-function($value)`**

  Check if a given value is a function name or reference and throw an error otherwise. See `sf-is-function` for informations on the expected value.

  You can use it to check for your user arguments like:
  ```scss
  @function example($callback) {
    $_: sf-assert-function($callback);

    // ...your code with $callback secured..
  }
  ```

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

* **`sf-get-function($func)`**

  Return a reference to the given function or a function name string so it is callable in the current Sass version. For Sass < 3.5, return the passed argument. For Sass >= 3.5, return a function reference if a function name string was passed.

  For example, use `sf-get-function` to get a function you can call no matter which Sass version is running.
  ```scss
  @function example($callback) {
    $safe-function: sf-get-function($callback);

    // ...your code with $safe-function secured..
  }
  ```

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
