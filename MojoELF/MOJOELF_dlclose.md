# MOJOELF_dlclose

Dispose of a previously-loaded ELF binary.

## Header File

Defined in [<mojoelf.h>](https://github.com/icculus/mojoelf/blob/main/mojoelf.h)

## Syntax

```c
void MOJOELF_dlclose(void *lib);
```

## Function Parameters

|        |         |                                     |
| ------ | ------- | ----------------------------------- |
| void * | **lib** | the ELF binary of which to dispose. |

## Remarks

This will free any resources involved with this ELF binary, including
calling into a [MOJOELF_UnloaderCallback](MOJOELF_UnloaderCallback) to
clean out any dependencies that were loaded with the binary.

The `lib` param must be a pointer returned from
[MOJOELF_dlopen_mem](MOJOELF_dlopen_mem)() or
[MOJOELF_dlopen_file](MOJOELF_dlopen_file)(). You can not use a handle
returned from the C runtime's dlopen() function here!

MojoELF does not currently reference-count loaded ELF binaries; a single
call to this function will destroy the binary's handle (and multiple loads
of the same library will all be separate instances of it, that are closed
separately). Once this function is called, the app should consider `lib`
invalid and not use it again.

Calling this function with a NULL `lib` is a valid no-op.

## Thread Safety

this function is not thread-safe.

## Version

This function is available since MojoELF 1.0.0.

## See Also

- [MOJOELF_dlopen_mem](MOJOELF_dlopen_mem)
- [MOJOELF_dlopen_file](MOJOELF_dlopen_file)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryMojoELF](CategoryMojoELF)

