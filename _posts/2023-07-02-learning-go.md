---
layout: post
title: Go Notes
excerpt_image: ../../../../assets/images/gopher.png
categories: Backend
tags: [backend, basic]
---

# Learning Go By Jon Bodner

`var` vs `:=` 
Both of them are used to declare the variables, but they are slight different from each other.
* `var` can be used at package level declaration, but `:=` can only be used inside the function
* `:=` can be use to redeclare the value. For example, `a, b := "a", "b"` even if `a` or `b` has been declared before. However, it is not allowed when using `var`

`array` vs `slice`
* Go considers size of the `array` to be part of the type of the array which means `[3]int` is different from `[4]int`. And type must be resolved at compile time not runtime time. Normally array is not recommended to use unless you know the exact size of the array at the beginning. for example in some cryptographic algorithm.
* `slice` has more flexibily to increase the capacity of the array.
* the length and capacity are two different concepts in `slice`. When the length exceeds capacity, Go will double the capacity and copy the slice to a new memory address. GC handles the original one.
* memory sharing properties in `slice` and `array`
* use `copy` to create a slice that independent of original


`map` vs `set`

* Go doesn't include `set`, use `map` to simulate the behaviour of a set


shadowing variables
* if variable redeclare inside a statement with `var` or `:=`, the value remains the same as the one declared before the statement after the statement is destoryed
* install `shadow` (`go install golang.org/x/tools/go/analysis/passes/shadow/cmd/shadow@latest`) to detect shadow variables