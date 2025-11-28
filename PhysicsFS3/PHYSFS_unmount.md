# PHYSFS_unmount

Remove a directory or archive from the search path.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_unmount(const char *oldDir);
```

## Function Parameters

|              |            |                        |
| ------------ | ---------- | ---------------------- |
| const char * | **oldDir** | dir/archive to remove. |

## Return Value

(int) Returns nonzero on success, zero on failure. Use
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to obtain the specific
error.

## Remarks

This is functionally equivalent to
[PHYSFS_removeFromSearchPath](PHYSFS_removeFromSearchPath)(), but that
function is deprecated to keep the vocabulary paired with
[PHYSFS_mount](PHYSFS_mount)().

This must be a (case-sensitive) match to a dir or archive already in the
search path, specified in platform-dependent notation.

This call will fail (and fail to remove from the path) if the element still
has files open in it.

**WARNING**: This function wants the path to the archive or directory that
was mounted (the same string used for the "newDir" argument of
[PHYSFS_addToSearchPath](PHYSFS_addToSearchPath) or any of the mount
functions), not the path where it is mounted in the tree (the "mountPoint"
argument to any of the mount functions).

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_getSearchPath](PHYSFS_getSearchPath)
- [PHYSFS_mount](PHYSFS_mount)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

