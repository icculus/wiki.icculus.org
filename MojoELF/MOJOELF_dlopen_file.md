# MOJOELF_dlopen_file

Dynamically load an ELF binary from a path on the filesystem.

## Header File

Defined in [<mojoelf.h>](https://github.com/icculus/mojoelf/blob/main/mojoelf.h)

## Syntax

```c
void * MOJOELF_dlopen_file(const char *fname, const MOJOELF_Callbacks *cb);
```

## Function Parameters

|                                                |           |                                                                                                                                       |
| ---------------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| const char *                                   | **fname** | the path to the file to load on the filesystem.                                                                                       |
| const [MOJOELF_Callbacks](MOJOELF_Callbacks) * | **cb**    | callbacks that manage how the ELF loader operates. May be NULL, and any function pointer in the struct may also individually be NULL. |

## Return Value

(void *) Returns a non-NULL pointer on success, NULL on failure. On
failure, a human-readable error message may be obtained by calling
[MOJOELF_dlerror](MOJOELF_dlerror)().

## Remarks

This is a convenience function that allocates a temporary memory buffer,
loads `fname` into it, calls [MOJOELF_dlopen_mem](MOJOELF_dlopen_mem)(),
and then frees the temporary buffer.

All the same information in that function's documentation applies here.

## Thread Safety

this function is not thread-safe.

## Version

This function is available since MojoELF 1.0.0.

## See Also

- [MOJOELF_dlopen_mem](MOJOELF_dlopen_mem)
- [MOJOELF_dlsym](MOJOELF_dlsym)
- [MOJOELF_dlclose](MOJOELF_dlclose)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryMojoELF](CategoryMojoELF)

