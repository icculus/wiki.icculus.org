# MOJOELF_getentry

Obtain an ELF binary's official entry point.

## Header File

Defined in [<mojoelf.h>](https://github.com/icculus/mojoelf/blob/main/mojoelf.h)

## Syntax

```c
const void * MOJOELF_getentry(void *lib);
```

## Function Parameters

|        |         |                                                         |
| ------ | ------- | ------------------------------------------------------- |
| void * | **lib** | a handle from a MojoELF-opened ELF binary. May be NULL. |

## Return Value

(const void *) Returns the address of the ELF binary's entry point.

## Remarks

You almost certainly do not want or need this function.

This returns the address where a process should start executing (which
would, in most cases, perform some initialization code that eventually
calls the `main` function).

Not all ELF binaries have an entry point, in which case this will return
NULL, but this scenario is not an error in itself. Shared libraries, the
most common thing one would load, often do not have an entry point (but
they may! One can run glibc's libc.so on a Linux box as if it were a
program and it will print information to stdout.) Binaries meant to be run
as standalone programs always have an entry point, out of necessity.

ELF binaries might have initialization code that runs at load time (DT_INIT
sections, etc), which is unrelated to the entry point, and is handled
during [MOJOELF_dlopen_mem](MOJOELF_dlopen_mem)() or
[MOJOELF_dlopen_file](MOJOELF_dlopen_file)().

If you are looking to load a shared library and call into a function in it,
this is not the function you should call. Instead, obtain the function's
address through a call to [MOJOELF_dlsym](MOJOELF_dlsym)(). This function
is useful if you want to load and run an ELF program, which has other
complications beyond just calling into a function pointer.

Passing in a NULL `lib` will return NULL.

## Thread Safety

this function is not thread-safe.

## Version

This function is available since MojoELF 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryMojoELF](CategoryMojoELF)

