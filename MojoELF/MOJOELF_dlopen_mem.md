# MOJOELF_dlopen_mem

Dynamically load an ELF binary from memory.

## Header File

Defined in [<mojoelf.h>](https://github.com/icculus/mojoelf/blob/main/mojoelf.h)

## Syntax

```c
void * MOJOELF_dlopen_mem(const void *buf, const long buflen, const MOJOELF_Callbacks *cb);
```

## Function Parameters

|                                                |            |                                                                                                                                       |
| ---------------------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| const void *                                   | **buf**    | the bytes of a valid ELF binary to be loaded.                                                                                         |
| const long                                     | **buflen** | the number of bytes pointed to by `buf`.                                                                                              |
| const [MOJOELF_Callbacks](MOJOELF_Callbacks) * | **cb**     | callbacks that manage how the ELF loader operates. May be NULL, and any function pointer in the struct may also individually be NULL. |

## Return Value

(void *) Returns a non-NULL pointer on success, NULL on failure. On
failure, a human-readable error message may be obtained by calling
[MOJOELF_dlerror](MOJOELF_dlerror)().

## Remarks

This will load binary's code and data into appropriate places in the
address space, load any dependencies it specifies as well, fixup any
symbols necessary, and prepare a table of exported symbols for later
lookup.

If there is initialization code in the ELF binary (a DT_INIT section, etc),
and the loading was otherwise successful, that code will run before this
function returns.

Callbacks are not required (any specific function may safely be NULL, and
the struct itself may be NULL as well), but loading an ELF of almost any
complexity will fail without a means to load dependencies and resolve
symbols in them.

On success, this returns an opaque handle to the newly-opened binary. On
failure, this returns NULL, and [MOJOELF_dlerror](MOJOELF_dlerror)() can be
used to get a human-readable reason why.

A valid handle can than be used with [MOJOELF_dlsym](MOJOELF_dlsym)() to
find the location of the ELF's symbols in memory, such as to find a
function pointer to call through.

When done with the returned handle, pass it to
[MOJOELF_dlclose](MOJOELF_dlclose)() to dispose of it. The pointer returned
here is not compatible with the C runtime's dlclose(), dlsym(), etc; only
use it with MojoELF functions!

This function copies the data in `buf` as appropriate; the original buffer
can be disposed of once this function returns.

## Thread Safety

this function is not thread-safe.

## Version

This function is available since MojoELF 1.0.0.

## See Also

- [MOJOELF_dlopen_file](MOJOELF_dlopen_file)
- [MOJOELF_dlsym](MOJOELF_dlsym)
- [MOJOELF_dlclose](MOJOELF_dlclose)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryMojoELF](CategoryMojoELF)

