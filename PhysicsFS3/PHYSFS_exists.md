# PHYSFS_exists

Determine if a file exists in the search path.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_exists(const char *fname);
```

## Function Parameters

|              |           |                                            |
| ------------ | --------- | ------------------------------------------ |
| const char * | **fname** | filename in platform-independent notation. |

## Return Value

(int) Returns non-zero if filename exists. zero otherwise.

## Remarks

Reports true if there is an entry anywhere in the search path by the name
of `fname`.

Note that entries that are symlinks are ignored if
[PHYSFS_permitSymbolicLinks](PHYSFS_permitSymbolicLinks)(1) hasn't been
called, so you might end up further down in the search path than expected.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

