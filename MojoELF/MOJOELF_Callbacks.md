# MOJOELF_Callbacks

A struct for passing a set of callbacks into MojoELF.

## Header File

Defined in [<mojoelf.h>](https://github.com/icculus/mojoelf/blob/main/mojoelf.h)

## Syntax

```c
typedef struct MOJOELF_Callbacks
{
    MOJOELF_LoaderCallback loader;
    MOJOELF_ResolverCallback resolver;
    MOJOELF_UnloaderCallback unloader;
} MOJOELF_Callbacks;
```

## Remarks

This exists to gather all callbacks up and pass a single pointer to the
dlopen functions.

## Version

This function is available since MojoELF 1.0.0.

## See Also

- [MOJOELF_dlopen_mem](MOJOELF_dlopen_mem)
- [MOJOELF_dlopen_file](MOJOELF_dlopen_file)

----
[CategoryAPI](CategoryAPI), [CategoryAPIStruct](CategoryAPIStruct), [CategoryMojoELF](CategoryMojoELF)

