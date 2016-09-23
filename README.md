# Modern C++ Style Guidelines

Modern C++ style guidelines, as per C++14 and later versions of the language.

These guidlines are based on several resources:

* [Effective Modern C++ by Scott Meyers](https://www.amazon.co.uk/Effective-Modern-Specific-Ways-Improve/dp/1491903996)
* [C++ Seasoning by Sean Parent](https://channel9.msdn.com/Events/GoingNative/2013/Cpp-Seasoning)
* [Peter Steinberger's C++ talk at altconf](https://realm.io/news/altconf-peter-steinberger-objective-c++-what-could-possibly-go-wrong/)

## Range-based `for` loops

Added in C++11, use them:
```
for (Item& item : vector) {
    doSomethingWith(item);
}
```

Avoid the vastly more verbose and cryptic C++98 way:
```
for (vector<Item>::iterator i = vector.begin(), e = v.end(); i != e; ++i) {
  doSomethingWith(*i);
}
```

## Memory management and pointers

Every `malloc` is a mistake.

## Type Inference

Use `auto` wherever you can.

## Lambdas

todo: examples

## Move semantics

todo: detail them
