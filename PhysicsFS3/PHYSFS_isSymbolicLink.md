# PHYSFS_isSymbolicLink

Determine if a file in the search path is really a symbolic link.

## Deprecated

As of PhysicsFS 2.1, use [PHYSFS_stat](PHYSFS_stat)() instead. This
function just wraps it anyhow.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_isSymbolicLink(const char *fname);
```

## Function Parameters

|              |           |                                            |
| ------------ | --------- | ------------------------------------------ |
| const char * | **fname** | filename in platform-independent notation. |

## Return Value

(int) Returns non-zero if filename exists and is a symlink. zero otherwise.

## Remarks

Determine if the first occurence of `fname` in the search path is really a
symbolic link.

Note that entries that are symlinks are ignored if
[PHYSFS_permitSymbolicLinks](PHYSFS_permitSymbolicLinks)(1) hasn't been
called, and as such, this function will always return 0 in that case.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_stat](PHYSFS_stat)
- [PHYSFS_exists](PHYSFS_exists)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

