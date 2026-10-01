# MOJOELF_DECL

A macro to tag a symbol as a public API.

## Header File

Defined in [<mojoelf.h>](https://github.com/icculus/mojoelf/blob/main/mojoelf.h)

## Syntax

```c
#define MOJOELF_DECL
```

## Remarks

MojoELF uses this macro for all its public functions. On some targets, it
is used to signal to the compiler that this function needs to be exported
from a shared library, but it might have other side effects.

Generally one compiles MojoELF into a project directly and doesn't
dynamically link it, so [MOJOELF_DECL](MOJOELF_DECL) is intentionally
blank.

It's here in case you _must_ override it for whatever reason, and because
wikiheaders.pl uses this to identify function signatures in this header
when generating documentation. You can probably ignore it.

## Version

This macro is available since MojoELF 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIMacro](CategoryAPIMacro), [CategoryMojoELF](CategoryMojoELF)

