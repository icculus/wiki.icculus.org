# MOJOELF_UnloaderCallback

A callback used when MojoELF is done with a dependency.

## Header File

Defined in [<mojoelf.h>](https://github.com/icculus/mojoelf/blob/main/mojoelf.h)

## Syntax

```c
typedef void (*MOJOELF_UnloaderCallback)(void *handle);
```

## Function Parameters

|            |                                                                                                       |
| ---------- | ----------------------------------------------------------------------------------------------------- |
| **handle** | a pointer returned from a previous [MOJOELF_LoaderCallback](MOJOELF_LoaderCallback), to be destroyed. |

## Remarks

This is called during [MOJOELF_dlclose](MOJOELF_dlclose)(), once for each
dependency that a [MOJOELF_LoaderCallback](MOJOELF_LoaderCallback)
successfully loaded. It will also be called during the `MOJOELF_dlopen_*`
functions if they fail, to clean up the half-initialized state.

The callback should dispose of any resources allocated during the paired
[MOJOELF_LoaderCallback](MOJOELF_LoaderCallback). After this call returns,
MojoELF will not use this copy of `handle` again.

## Thread Safety

This will be called from the same thread that called into
`MOJOELF_dlopen_*` or [MOJOELF_dlclose](MOJOELF_dlclose)(). Locking is not
provided by MojoELF.

## Version

This function is available since MojoELF 1.0.0.

## See Also

- [MOJOELF_ResolverCallback](MOJOELF_ResolverCallback)
- [MOJOELF_UnloaderCallback](MOJOELF_UnloaderCallback)

----
[CategoryAPI](CategoryAPI), [CategoryAPIDatatype](CategoryAPIDatatype), [CategoryMojoELF](CategoryMojoELF)

