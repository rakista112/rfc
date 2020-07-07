# Naming convention in ArkScript

This RFC is targetting naming convention in the standard library, builtins and modules, to have something uniformised.

*Last modification on the 07/07/2020 at 16:22*

## Definitions

_guideline_: general rule applying to ArkScript code, which must be followed when contributing to the standard library and examples of the main repository
_standard library (aka lib)_: the files and functions in the `lib` folder
_builtins_: functions and constants defined through C++ code, available without having to import anything
_module_: C++ plugin for the ArkScript virtual machine, allowing use of C++ code (eg: the SFML)

## Naming

It should follow `first:second`, where `first` is related to the module, builtin or lib function area of effect. `second` should be the name of the function it self.

We can see this kind of method as *namespacing* in other languages such as C++.

Example:
```clojure
# for math functions
(math:sin 0.5421)

# for list functions
(list:forEach the-list (fun (element) (...)))

# for a console module
(console:color "red")
```

# Authors

* [Alexandre Plateau](https://github.com/SuperFola)