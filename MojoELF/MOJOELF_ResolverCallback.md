# MOJOELF_ResolverCallback

A callback used when MojoELF needs to resolve a symbol.

## Header File

Defined in [<mojoelf.h>](https://github.com/icculus/mojoelf/blob/main/mojoelf.h)

## Syntax

```c
typedef void *(*MOJOELF_ResolverCallback)(void *handle, const char *sym);
```

## Function Parameters

|            |                                                                                                                                          |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **handle** | a pointer returned from a previous [MOJOELF_LoaderCallback](MOJOELF_LoaderCallback), or NULL when all other options have been exhausted. |
| **sym**    | the symbol to find an address for.                                                                                                       |

## Return Value

Returns address of symbol if found, NULL if symbol isn't available.

## Remarks

This passes the pointer returned by
[MOJOELF_LoaderCallback](MOJOELF_LoaderCallback) as `handle` and will call
this callback once for each loaded library until it finds one that resolves
the symbol or runs out of libraries to try.

The callback is called once for each non-NULL value that your loader
previously returned, in the other they were returned, until one succeeds.
If none succeeds, the callback fires one more time with the handle set to
NULL. If this still doesn't return a non-NULL value, MojoELF will give up
on the ELF file it was in the process of loading, due to missing
dependencies.

A simple resolver callback might look like this:

```c
extern int my_function(int argument);

void *my_resolver(void *handle, const char *sym)
{
  if (strcmp(sym, "my_function") == 0)
      return my_function;
  // this also works for data, not just functions.
  return NULL;  // can't help you.
}
```

As you can see, it isn't _required_ to build a whole resolving
infrastructure if one just wants to provide a handful of specific entry
points.

Note: this callback returns NULL to specify "symbol not found" but strictly
speaking, a symbol _could_ exist at address 0x00000000. In practice, this
would be ridiculous, so MojoELF makes no effort to allow this scenario.

## Thread Safety

This will be called from the same thread that called into
`MOJOELF_dlopen_*`. Locking is not provided by MojoELF.

## Version

This function is available since MojoELF 1.0.0.

## See Also

- [MOJOELF_LoaderCallback](MOJOELF_LoaderCallback)
- [MOJOELF_UnloaderCallback](MOJOELF_UnloaderCallback)

----
[CategoryAPI](CategoryAPI), [CategoryAPIDatatype](CategoryAPIDatatype), [CategoryMojoELF](CategoryMojoELF)

