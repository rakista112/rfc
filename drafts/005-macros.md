# ArkScript macros - DRAFT

*feel free to provide examples if you think something can be unclear*

## Definitions

_macro_: a fragment of code which has been given a name. Whenever the name is used, it is replaced by the contents of the macro. They are two kinds of macros: objects-like macros and functions-like macros.

_object-like macro_: ressemble data object when used

_function-like macro_: ressemble function call when used

_preprocessor_: system which handles the macro application process

## Precisions

*remove if empty, not necessary in the draft*

## Elimination of macros

Macros should be applied in the order they appear after parsing ArkScript code.

Every macro, used or not, should be eliminated from the source code before sending the code to the optimizer.

The preprocessor should run right after the parsing and before the optimizer.

## Syntax

### Object-like macro

```
!{name body}
```

`name` will be replaced by `body` when used in ArkScript code.

### Function-like macro

```
!{name (args) body}
```

`(name args...)` should be replaced by `body` when used in ArkScript code. The number of arguments sent to the macro should be checked, and if it's wrong, it should be reported and should abort the compilation process.

### Variadic arguments

We introduce the notation `...name` to tell the preprocessor that `name` will be a list of all the other arguments given to a macro. Using the triple-dot notation before an argument name terminates the argument list.

Example:

```clojure
# valid
!{foo (...name) body}

# valid
!{foo (a b c ...name) body}

# invalid, ...name isn't the last element
!{foo (a b ...name c) body}
```

The list of argument created by `...name` will result in a real ArkScript list at runtime, and will be manipulated as one, thus notations like
* `(len name)`
* `(@ name 1)`
* ...

are valid.

## Macro definition rules

1. macros can only be defined at the root level of the AST, thus defining a macro inside a `let` statement (for example) is an error
1. following the previous rule, macros can not be nested (a macro defined inside a macro)
1. macros can be chained:
```clojure
# first, foo is applied, and the macro bar is modified
!{foo 1}
# then, bar is applied
!{bar (egg) (+ foo egg)}

(let a (bar 1))
```

# Authors

(add your name here)

* [Alexandre Plateau](https://github.com/SuperFola)