# MOJOELF_CALL

The calling conventions for MojoELF entry points.

## Header File

Defined in [<mojoelf.h>](https://github.com/icculus/mojoelf/blob/main/mojoelf.h)

## Syntax

```c
#define MOJOELF_CALL
```

## Remarks

This is currently defined to nothing on all platforms and compilers. As
such, at this time it means all APIs and callbacks use the compiler's
default calling conventions ("cdecl" or whatever).

This is for future expansion, and compatibility with wikiheaders.pl.

## Version

This macro is available since MojoELF 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIMacro](CategoryAPIMacro), [CategoryMojoELF](CategoryMojoELF)

