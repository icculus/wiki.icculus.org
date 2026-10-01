# MOJOELF_dlsym

Lookup a symbol in an ELF binary.

## Header File

Defined in [<mojoelf.h>](https://github.com/icculus/mojoelf/blob/main/mojoelf.h)

## Syntax

```c
void * MOJOELF_dlsym(void *lib, const char *sym);
```

## Function Parameters

|              |         |                                            |
| ------------ | ------- | ------------------------------------------ |
| void *       | **lib** | a handle from a MojoELF-opened ELF binary. |
| const char * | **sym** | the symbol to look up.                     |

## Return Value

(void *) Returns non-NULL address of the symbol if found, NULL if not
found. On failure, a human-readable error message may be obtained by
calling [MOJOELF_dlerror](MOJOELF_dlerror)().

## Remarks

The `lib` param must be a pointer returned from
[MOJOELF_dlopen_mem](MOJOELF_dlopen_mem)() or
[MOJOELF_dlopen_file](MOJOELF_dlopen_file)(). You can not use a handle
returned from the C runtime's dlopen() function here!

A NULL return value means the symbol was not found. Strictly speaking,
though, a symbol _could_ have a valid address of NULL--zero--but this is
not allowed in MojoELF, and would be extremely foolish anyhow.

## Thread Safety

this function is not thread-safe.

## Version

This function is available since MojoELF 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryMojoELF](CategoryMojoELF)

