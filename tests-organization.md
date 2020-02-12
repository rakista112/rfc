# Tests organization

*Last modification on the 12/02/2020 at 10:50*

## Defintions

_module_: either a file at the root of the `lib` folder or a folder at the root of the aforementioned folder
_test_: a file in the `tests` folder, named as following: `ABC-tests.ark`, `ABC` being the test's name.

## Precisions

Each test should target a single module.

## Content of a test file

A test should import `test-tools.ark`, a small utility to count passed tests and do nice recaps.

If the test targets a module, for example the `string` module, it should import all the files composing the aforementioned module.

Then the content of the test is wrapped up in a function taking no arguments, to create a fresh scope for testing purposes, thus avoiding possible collisions between multiple tests, since all the tests are imported and launched in a single file, `unittests.ark`.

A tests counter must be defined as `(mut tests 0)` since the utility function `assert_` located in `test-tools.ark` will increment it each time an assertion is executed without errors ; a time point must also be set at the begining of the testing function, to know how long the tests took: `(let start-time (time))`.

An assertion is written like so: `(assert_ condition error-message-in-case-of-failure)`.

The last function to call is `recap`, defined in `test-tools.ark`: it will take the test name, the number of assertions passed, and a time difference in seconds, like so: `(recap "Math tests passed" tests (- (time) start-time))`.

Then the function should return the value of `tests`, which will be retrieved in a variable at the bottom of the file: `(let passed-ABC (ABC-tests))`, `ABC` being the name of the tests. The variable `passed-ABC` will be used in `unittests.ark` to increment a global tests counter.

The newly written test should then be imported by `unittests.ark`.

# Authors

* [Alexandre Plateau](https://github.com/SuperFola)