# Modern C++ Style Guidelines

Modern C++ style guidelines, as per C++14 and later versions of the language.

From: [A Brief, Incomplete, and Mostly Wrong History of Programming Languages](http://james-iry.blogspot.co.uk/2009/05/brief-incomplete-and-mostly-wrong.html)

> 1972 - Dennis Ritchie invents a powerful gun that shoots both forward and backward simultaneously. Not satisfied with the number of deaths and permanent maimings from that invention he invents C and Unix.

> ...

> 1983 - Bjarne Stroustrup bolts everything he's ever heard of onto C to create C++. The resulting language is so complex that programs must be sent to the future to be compiled by the Skynet artificial intelligence.

C++ is a minefield. This document is designed as a guide to negotiate that minefield, so that your C++ code can be 'least insane'.


These guidlines are based on several resources:

* [Effective Modern C++ by Scott Meyers](https://www.amazon.co.uk/Effective-Modern-Specific-Ways-Improve/dp/1491903996)
* [C++ Seasoning by Sean Parent](https://channel9.msdn.com/Events/GoingNative/2013/Cpp-Seasoning)
* [Peter Steinberger's C++ talk at altconf](https://realm.io/news/altconf-peter-steinberger-objective-c++-what-could-possibly-go-wrong/)

## General

Use `#pragma once` rather than manual `#ifndef ...` boilderplate for ensuring headers are only included once.

## Strings

Use `std::string` for string handling.

If you do this:
```
#include <iostream>
using namespace std;
```
Then you can write this:
`string someName = "Barry";`

## Type Inference

Use `auto` wherever you can.

## Range-based `for` loops

Added in C++11, use them:
```
for (auto& item : vector) {
    doSomethingWith(item);
}
```

Avoid the vastly more verbose and cryptic C++98 way:
```
for (vector<Item>::iterator i = vector.begin(), e = v.end(); i != e; ++i) {
    doSomethingWith(*i);
}
```

## Vectors

Should be your go-to collection type:
* Continuous in memory.
* Can exist on the stack or heap.
* Out of bounds exceptions.
* Have powerful mutators like `rotate`.

Use initialiser lists:
`std::vector<int> v = { 1, 2, 3, 4 };`

Use `emplace_back` to add a new element (as of C++14).

## Memory management and pointers

* Every `malloc` and `free` is a mistake.
* Every `new` and `delete` is a mistake.
* Avoid `auto_ptr`, it is C++98 legacy cruft at this point, forget it exists.

Use smart pointers:
* `unique_ptr` - if the object is unique.
* `shared_ptr` - if you share an object.
* `weak_ptr` - other, rarer scenarios.

Use `make_unique` to allocate a unique pointer.

```
vector<unique_ptr<Person>> get_People();

auto people = get_People();
people.emplace_back(make_unique<Person>("Bob"));
shared_ptr<Person> bob = people[0];
```

## Move semantics

`vector<Point> points = getPoints();`

The following will do a move, not a copy (note the `&&` operator in the method signature):
```
vector(vector&& that) {
    data = that.data;
    that.data = nullptr;
}
```

## Lambdas

todo: examples


