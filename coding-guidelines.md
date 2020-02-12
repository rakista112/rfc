# Coding guidelines

*Last modification on the 12/02/2020 at 10:49*

## Definitions

_guideline_: general rule applying to ArkScript code, which must be followed when contributing to the standard library and examples of the main repository
_standard library (aka lib)_: the files and functions in the `lib` folder
_builtins_: functions and constants defined through C++ code, available without having to import anything
_module_: C++ plugin for the ArkScript virtual machine, allowing use of C++ code (eg: the SFML)

## Precisions

Indentation matters to us, programmers (but not to the compiler): 4 spaces or a single tab, but it should stay consistent accross a project/file.

## Naming convention

Functions (the ones in the lib and in the builtins) are named following the camelCase, same goes for modules' functions.

Constants (the ones in the lib and in the builtins) are named following the PascalCase, same goes for modules' constants.

## Block definitions

* Indent the content of every `begin` block
* When a `begin` block is closed and a new one is opened in the same expression, they should be on the same line. eg:
```
# ok:
... } { ...
# also ok:
... ) (begin ...

# not ok:
... }
{ ...
# not ok:
... )
(begin ...
```

Complete example:

```clojure
(let foo (fun (a) {
    (if (= a 2) {
        (print "a = 2")
        (egg (* 2 a))
    } {
        (print "a != 2")
        (egg 0)
    })
}))
```

## Standard library functions and constants' documentation

Each function and constant defined in the standard library should be documented.

- The type of the symbol (alongside its name) should be mentionned in a comment on the same line.
- If it is a **constant**, the next line (a comment as well) should mention the role/use of this symbol
- If it is a **function**:
    - the next line should mention the types of each of the arguments
    - another line to explain the role/use of the symbol (if needed, more lines can be added for this specific part)

Example:

```clojure
# ANiceConst: Number
# The number of pills Morpheus is offering to Neo
(let ANiceConst 2)

# justDoIt: Function
# a: Number, b: String, c: List of Numbers
# Returns string at ((sum of a with length of b) mod length of c) in c
(let justDoIt (fun (a b c) { body...}))
```

# Authors

* [Alexandre Plateau](https://github.com/SuperFola)