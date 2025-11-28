# PHYSFS_enumerateFiles

Get a file listing of a search path's directory.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
char ** PHYSFS_enumerateFiles(const char *dir);
```

## Function Parameters

|              |         |                                                          |
| ------------ | ------- | -------------------------------------------------------- |
| const char * | **dir** | directory in platform-independent notation to enumerate. |

## Return Value

(char **) Returns Null-terminated array of null-terminated strings, or NULL
for failure cases.

## Remarks

**WARNING**: In PhysicsFS versions prior to 2.1, this function would return
as many items as it could in the face of a failure condition (out of
memory, disk i/o error, etc). Since this meant apps couldn't distinguish
between complete success and partial failure, and since the function could
always return NULL to report catastrophic failures anyway, in PhysicsFS 2.1
this function's policy changed: it will either return a list of complete
results or it will return NULL for any failure of any kind, so we can
guarantee that the enumeration ran to completion and has no gaps in its
results.

Matching directories are interpolated. That is, if "C:\mydir" is in the
search path and contains a directory "savegames" that contains "x.sav",
"y.sav", and "z.sav", and there is also a "C:\userdir" in the search path
that has a "savegames" subdirectory with "w.sav", then the following code:

```c
char **rc = PHYSFS_enumerateFiles("savegames");
for (char **i = rc; *i != NULL; i++) {
    printf(" * We've got [%s].\n", *i);
}
PHYSFS_freeList(rc);
```

will print:

```
We've got [x.sav].
We've got [y.sav].
We've got [z.sav].
We've got [w.sav].
```

Feel free to sort the list however you like. However, the returned data
will always contain no duplicates, and will be always sorted in alphabetic
(rather: case-sensitive Unicode) order for you.

Don't forget to call [PHYSFS_freeList](PHYSFS_freeList)() with the return
value from this function when you are done with it.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_enumerate](PHYSFS_enumerate)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

