---
layout: reference
permalink: /reference/
---

## [First session with GAP](01-command-line.html)

* [GAP Tutorial: A First session with GAP](http://www.gap-system.org/Manuals/doc/tut/chap2.html)

* [GAP Reference Manual: Naming Conventions](https://plus.google.com/events/cfm3tc375c142qtodvlvcfs82l4)

* [GAP Reference Manual: The Help System](http://www.gap-system.org/Manuals/doc/ref/chap2.html)

* [GAP Tutorial: Lists and Records](http://www.gap-system.org/Manuals/doc/tut/chap3.htm)

* [GAP Reference Manual: Strings and Characters](http://www.gap-system.org/Manuals/doc/ref/chap27.html)

* [GAP Reference Manual: The Programming Language]( http://www.gap-system.org/Manuals/doc/ref/chap4.html#X7FE7C0C17E1ED118)


## [Some more GAP objects](02-some-objects.html)

* [Integers](http://www.gap-system.org/Manuals/doc/ref/chap14.html)

* [Rationals](http://www.gap-system.org/Manuals/doc/ref/chap17.html)

* [Cyclotomic numbers](http://www.gap-system.org/Manuals/doc/ref/chap18.html)

* [Floats](http://www.gap-system.org/Manuals/doc/ref/chap19.html)

* [Finite Field Elements](http://www.gap-system.org/Manuals/doc/ref/chap59.html)

* [Permutations](http://www.gap-system.org/Manuals/doc/ref/chap42.html)

* [Lists](http://www.gap-system.org/Manuals/doc/ref/chap21.html)

* [Records](http://www.gap-system.org/Manuals/doc/ref/chap29.html)

* [Strings and Characters](http://www.gap-system.org/Manuals/doc/ref/chap27.html)


## [Functions in GAP](03-func.html)

* [GAP Tutorial: Functions](http://www.gap-system.org/Manuals/doc/tut/chap4.html)


## [Using regression tests](04-testing.html)

* [GAP Reference Manual: Test](http://www.gap-system.org/Manuals/doc/ref/chap7.html#X87712F9D8732193C)


## [Small groups search](05-small-groups.html)

* [GAP Reference Manual: Group Libraries](http://www.gap-system.org/Manuals/doc/ref/chap50.html)


## [Attributes and Methods](06-attributes.html)

* [GAP Tutorial: Operations and Methods](http://www.gap-system.org/Manuals/doc/tut/chap8.html)

* [GAP Reference Manual: Adding a new Attribute](http://www.gap-system.org/Manuals/doc/ref/chap80.html#X874AF11D864AEC1B)

## Glossary

Attribute
:    Operation (normally, one-argument), the result of which is stored in its
     argument and cannot be changed any more.

List
:    Data structure whose elements are indexed by their _position_ in the list.

Method
:    Function that will be called for an operation for arguments of the
     specified type.

Operation
:    GAP function for which several _methods_ may be available (the particular
     method that will be used depends on the type of the arguments).

Property
:    Boolean-valued attribute

Record
:    Data structure which is a collection of _components_, each having a unique
     _name_, which is an _identifier_ that distinguishes this component, and a
     _value_, which is an object of arbitrary type.

Regression testing
:    Testing based on rerunning previously completed tests to check that new
     changes do not impact their correctness or worsen their performance.
