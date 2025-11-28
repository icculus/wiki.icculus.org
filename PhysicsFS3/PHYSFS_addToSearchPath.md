# PHYSFS_addToSearchPath

Add an archive or directory to the search path.

## Deprecated

As of PhysicsFS 2.0, use [PHYSFS_mount](PHYSFS_mount)() instead. This
function just wraps it anyhow.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_addToSearchPath(const char *newDir, int appendToPath);
```

## Function Parameters

|              |                  |                                                                          |
| ------------ | ---------------- | ------------------------------------------------------------------------ |
| const char * | **newDir**       | directory or archive to add to the path, in platform-dependent notation. |
| int          | **appendToPath** | nonzero to append to search path, zero to prepend.                       |

## Return Value

(int) Returns nonzero if added to path, zero on failure (bogus archive, dir
missing, etc). Use [PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to
obtain the specific error.

## Remarks

This function is equivalent to:

```c
PHYSFS_mount(newDir, NULL, appendToPath);
```

You must use this and not [PHYSFS_mount](PHYSFS_mount) if binary
compatibility with PhysicsFS 1.0 is important (which it may not be for many
people).

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_mount](PHYSFS_mount)
- [PHYSFS_removeFromSearchPath](PHYSFS_removeFromSearchPath)
- [PHYSFS_getSearchPath](PHYSFS_getSearchPath)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

