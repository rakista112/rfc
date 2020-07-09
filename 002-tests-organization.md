# Tests organization

*Last modification on the 09/07/2020 at 16:00*

## Defintions

_module_: either a file at the root of the `lib` folder or a folder at the root of the aforementioned folder
_test_: a file in the `tests` folder, named as following: `ABC-tests.ark`, `ABC` being the test's name.

## Precisions

Each test should target a single module.

## Content of a test file

A test should import `tests-tools.ark`, a small utility to count passed tests and do nice recaps.

If the test targets a module, for example the `string` module, it should import all the files composing the aforementioned module.

Then the content of the test is wrapped up in a function taking no arguments, to create a fresh scope for testing purposes, thus avoiding possible collisions between multiple tests, since all the tests are imported and launched in a single file, `unittests.ark`.

The basic architecture of a test file is as follows:

```clojure
(import "tests-tools.ark")

(let vm-tests (fun () {
    (mut tests 0)
    (let start-time (time))

    # the tests are here
    (set tests (assert-eq (+ 1 2) 3 "VM operations" tests))

    # the recap
    (recap "VM operations passed" tests (- (time) start-time))
    # return value
    tests
}))

(let passed-vm (vm-tests))
```

We must do a `(set tests (assert-function arguments...))` because the asserts functions all increment the tests count if it passed.

The different asserts functions are the following ones:
* `assert-eq`, arguments: `val1 val2 message tests`
* `assert-neq`, arguments: `val1 val2 message tests`
* `assert-gt`, arguments: `val1 val2 message tests`
* `assert-ge`, arguments: `val1 val2 message tests`
* `assert-lt`, arguments: `val1 val2 message tests`
* `assert-le`, arguments: `val1 val2 message tests`
* `assert-val`, arguments: `val0 message tests`

`val0`, `val1`, `val2` are the value to test, the `message` is the test name (useful if the test failed), and `tests` is the number of current passed tests.

The last function to call is `recap`, defined in `tests-tools.ark`: it will take the test name, the number of assertions passed, and a time difference in seconds, like so: `(recap "Math tests passed" tests (- (time) start-time))`.

Then the function should return the value of `tests`, which will be retrieved in a variable at the bottom of the file: `(let passed-ABC (ABC-tests))`, `ABC` being the name of the tests. The variable `passed-ABC` will be used in `unittests.ark` to increment a global tests counter.

The newly written test should then be imported by `unittests.ark`, and the `passed-ABC` variable should be added to the global tests counter in the same file.

# Authors

* [Alexandre Plateau](https://github.com/SuperFola)