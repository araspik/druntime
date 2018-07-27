DRuntime: Runtime Library for the D Programming Language
========================================================

This is a collection of things that people hacking on
DRuntime will want to know.

Code style
----------

The original DRuntime follows [this](https://dlang.org/dstyle.html).
This version only notes two exceptions:
* For whitespace, hardware tabs should be used
* Opening braces *do not* have their own line.
Please stick to everything in the style guide aside from the two
above exceptions noted, including the section on Phobos.

Publicity of modules
--------------------

In general, only modules in the 'core' package should be
made public. The single exception is the 'object' module
which is not in any package.

The convention is to put private modules in the 'rt' or
'gc' packages depending on what they do and only put
public modules in 'core'.

Ensure that no defined private modules (such as those in
'rt' and 'gc') are publicly imported by public-defined
module (such as those in 'core').

Adding new modules
------------------

If adding platform-dependent modules, remember to update
`CMakePlatformFiles.txt`.

Operating system bindings
-------------------------

Even though this fork of DRuntime does not explicitly
depend on any external items (such as the C library), it
will still provide the same support as provided by the
original DRuntime.

The 'core.sys' package provides bindings to most APIs
provided by supported operating systems.

The convention is to have OS-specific stuff in a
'core.sys.os' package where 'os' is the canonical name
for the OS (e.g. 'linux', 'osx', 'windows').

There is also the 'core.sys.posix' package in which
bindings to standardized POSIX APIs should be placed.
In this package, the convention is to put declarations
in sections based on the OS being compiled for. See
src/core/sys/posix/pwd.d for an example of how these
modules are arranged.

For all OS headers, it's a good idea to put a version
attribute at the top of the file containing the OS
the header is intended for. For example, in POSIX
modules, this would be 'version (Posix):' while in
Windows modules it would be 'version (Windows):' and
so on.

The convention is to have a D module per C header.

C99 bindings
------------

The 'core.stdc' package provides bindings to all C99
library types, functions, and macros. Unlike the style
in operating system bindings, bindings here should be
kept system-agnostic whenever possible.

Deprecation process
-------------------

Never remove a symbol without going through the proper
deprecation process.

When, for whatever reason, a symbol is to be deprecated,
annotate it as such using the 'deprecated' attribute. It
is a good idea to also provide a message on the attribute
so that the user can immediately see what symbol they
should use instead.

After six months of having been deprecated, a symbol can
be removed completely. It may also be kept around for
backwards compatibility if deemed necessary.

ABI breakage
------------

We're trying to get to a point where DRuntime's ABI is
completely stable and different compiler versions can
use different DRuntime versions. To this end, avoid
making ABI-breaking changes unless you have a *very*
good reason to do it.

Remember that renaming a symbol and leaving an alias
behind for the old symbol name *is* an ABI break. The
compiled name will be the new symbol, thus breaking old
binaries.

If it is absolutely required to rename a symbol, attempt
to leave an object-level alias for it, *not* just the
`alias`. It would be beneficial to join both:
```d
void newFoo(int a, int b);
@alias(newFoo) void oldFoo(int a, int b);
```
Unfortunately, this is just an idea until a system-agnostic
method can be developed. This is what it _would_ look like
once it is completed.

Updating the change log
-----------------------

If your pull request isn't a trivial bug fix, it
should be accompanied by a changelog entry explaining
the change in more details.
Please see the [`/changelog`](https://github.com/araspik/druntime/tree/master/changelog)
directory for detailed instructions.
DAutoTest will allow you and your reviewers to preview the rendered changelog entry.
