# PHYSFS_isDirectory

Determine if a file in the search path is really a directory.

## Deprecated

As of PhysicsFS 2.1, use [PHYSFS_stat](PHYSFS_stat)() instead. This
function just wraps it anyhow.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_isDirectory(const char *fname);
```

## Function Parameters

|              |           |                                            |
| ------------ | --------- | ------------------------------------------ |
| const char * | **fname** | filename in platform-independent notation. |

## Return Value

(int) Returns non-zero if filename exists and is a directory. zero
otherwise.

## Remarks

Determine if the first occurence of `fname` in the search path is really a
directory entry.

Note that entries that are symlinks are ignored if
[PHYSFS_permitSymbolicLinks](PHYSFS_permitSymbolicLinks)(1) hasn't been
called, so you might end up further down in the search path than expected.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_stat](PHYSFS_stat)
- [PHYSFS_exists](PHYSFS_exists)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

