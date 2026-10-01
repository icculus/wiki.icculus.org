# MOJOELF_Callbacks

A struct for passing a set of callbacks into MojoELF.

## Header File

Defined in [<mojoelf.h>](https://github.com/icculus/mojoelf/blob/main/mojoelf.h)

## Syntax

```c
typedef struct MOJOELF_Callbacks
{
    MOJOELF_LoaderCallback loader;  /**< loads dependencies during a dlopen */
    MOJOELF_ResolverCallback resolver;  /**< resolves dependencies during a dlopen */
    MOJOELF_UnloaderCallback unloader;  /**< unloads dependencies during dlclose */
} MOJOELF_Callbacks;
```

## Remarks

This exists to gather all callbacks up and pass a single pointer to the
dlopen functions.

## Version

This function is available since MojoELF 1.0.0.

## See Also

- [MOJOELF_LoaderCallback](MOJOELF_LoaderCallback)
- [MOJOELF_ResolverCallback](MOJOELF_ResolverCallback)
- [MOJOELF_UnloaderCallback](MOJOELF_UnloaderCallback)
- [MOJOELF_dlopen_mem](MOJOELF_dlopen_mem)
- [MOJOELF_dlopen_file](MOJOELF_dlopen_file)

----
[CategoryAPI](CategoryAPI), [CategoryAPIStruct](CategoryAPIStruct), [CategoryMojoELF](CategoryMojoELF)

