# MOJOELF_LoaderCallback

A callback used when MojoELF needs to load a new dependency.

## Header File

Defined in [<mojoelf.h>](https://github.com/icculus/mojoelf/blob/main/mojoelf.h)

## Syntax

```c
typedef void *(*MOJOELF_LoaderCallback)(const char *soname, const char *rpath, const char *runpath);
```

## Function Parameters

|             |                                                                                                                 |
| ----------- | --------------------------------------------------------------------------------------------------------------- |
| **soname**  | the SONAME of the ELF library to load.                                                                          |
| **rpath**   | the RPATH entry of the ELF library that needs this dependency. Will be NULL if the library had no such entry.   |
| **runpath** | the RUNPATH entry of the ELF library that needs this dependency. Will be NULL if the library had no such entry. |

## Return Value

Returns non-NULL on success, NULL on failure. The returned non-NULL pointer
must live until the paired
[MOJOELF_UnloaderCallback](MOJOELF_UnloaderCallback).

## Remarks

The "loader" callback doesn't necessarily load anything. All it does it
tell MojoELF that it's claiming a specific dependency. For example, if you
want to load an ELF that depends on libFoo.so.3, but you plan to override
this library without it actually existing, you can write a callback like
this...

```c
void *my_loader(const char *soname, const char *rpath, const char *runpath)
{
    return (void *) (strcmp(soname, "libFoo.so.3") == 0);
}
```

...and MojoELF will not try to load libFoo itself, and assumes you will
provide any needed symbols from it via your
[MOJOELF_ResolverCallback](MOJOELF_ResolverCallback).

Note that your loader can be significantly more complex...it could actually
_load_ something, for example, but for some projects, this is all that's
needed. What it chooses to load (even if it violates the norms of an ELF
loader) is entirely up to its discretion.

The loader callback is provided with any `RPATH` or `RUNPATH` entries in
the currently-loading ELF, in case finding the correct shared library might
need these. Please refer to Linux's `dlopen()` manpage for details on these
strings.

The value returned from the loader callback is opaque data. It will be
passed to your [MOJOELF_ResolverCallback](MOJOELF_ResolverCallback), and is
expected to be free'd in the
[MOJOELF_UnloaderCallback](MOJOELF_UnloaderCallback), if you like.

If this callback returns NULL, the library that MojoELF was in the process
of loading will fail to load in response.

## Thread Safety

This will be called from the same thread that called into
`MOJOELF_dlopen_*`. Locking is not provided by MojoELF.

## Version

This function is available since MojoELF 1.0.0.

## See Also

- [MOJOELF_ResolverCallback](MOJOELF_ResolverCallback)
- [MOJOELF_UnloaderCallback](MOJOELF_UnloaderCallback)

----
[CategoryAPI](CategoryAPI), [CategoryAPIDatatype](CategoryAPIDatatype), [CategoryMojoELF](CategoryMojoELF)

