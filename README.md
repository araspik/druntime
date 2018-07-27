DRuntime: Runtime Library for the D Programming Language
========================================================

This is DRuntime. It is the low-level runtime library
backing the D programming language.

This fork removes the need for a C library and provides
bare-metal support as well as support for common
platforms. It aims to be usable on all three major
compilers - DMD (may not have enough low-level support),
GDC, and LDC.

DRuntime is typically linked together with Phobos in a
release such that the compiler only has to link to a
single library to provide the user with the runtime and
the standard library.

However, this version is meant to be switchable-out so
that a compiler can compile code that can integrate with
C easily (for example, using the same allocators) or one
which can work bare-metal or standalone (no C interfacing).

Purpose
-------

DRuntime is meant to be an abstraction layer above the
compiler. Different compilers will likely have their
own versions of DRuntime. While the implementations
may differ, the interfaces should be the same.

This version goes beyond and tries to unify the compiler's
abstraction by providing support for all 3 major compilers.

Features
--------

The runtime library provides the following:

Note that in this fork, much of this will have to be rewritten in order to
remove dependencies on the C library and made as platform-independent as
possible. At the moment, very little works.

* The Object class, the root of the class hierarchy.
* Implementations of array operations.
* The associative array implementation.
* Type information and RTTI.
* Common threading and fiber infrastructure.
* Synchronization and coordination primitives.
* Exception handling and stack tracing.
* Garbage collection interface and implementation.
* Program startup and shutdown routines.
* Low-level math intrinsics and support code.
* Interfaces to standard C99 functions and types.
* Interfaces to operating system APIs.
* Atomic load/store and binary operations.
* CPU detection/identification for x86.
* System-independent time/duration functionality.
* D ABI demangling helpers.
* Low-level bit operations/intrinsics.
* Unit test, coverage, and trace support code.
* Low-level helpers for compiler-inserted calls.

Licensing
---------

See the [LICENSE.txt](https://github.com/araspik/druntime/blob/master/LICENSE.txt) file for licensing information.

Building
--------

The project is set up with CMake.
TODO: Nothing works right now.
