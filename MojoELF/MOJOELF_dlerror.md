# MOJOELF_dlerror

Obtain a human-readable error message for MojoELF problems.

## Header File

Defined in [<mojoelf.h>](https://github.com/icculus/mojoelf/blob/main/mojoelf.h)

## Syntax

```c
const char * MOJOELF_dlerror(void);
```

## Return Value

(const char *) Returns human-readable string of last error, or NULL if no
error has occured since the last call to this function.

## Remarks

This function returns a description of the last error that has occured in a
call to a MojoELF function.

The returned string is owned by MojoELF and should not be free'd by the
caller. This string lives at least until the next call into any of
MojoELF's functions.

Once a string is returned by this function, future calls to this function
will return NULL until another error has occured. If no error has _ever_
occured, NULL is returned. The correct usage pattern is to call this
immediately after receiving a failing result from a function call. It is
incorrect to call this function as a way to decide if a function call has
failed.

Note that MojoELF can be built so that this function always returns NULL,
which removes a lot of string data from the build, for minimizing the
program's binary size, etc. Doing this requires explicit intervention from
the app at build time, though, and is not the default.

## Thread Safety

this function is not thread-safe.

## Version

This function is available since MojoELF 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryMojoELF](CategoryMojoELF)

