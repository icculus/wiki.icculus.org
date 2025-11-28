# PHYSFS_setWriteDir

Tell PhysicsFS where it may write files.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_setWriteDir(const char *newDir);
```

## Function Parameters

|              |            |                                                                                                           |
| ------------ | ---------- | --------------------------------------------------------------------------------------------------------- |
| const char * | **newDir** | The new directory to be the root of the write dir, specified in platform-dependent notation. May be NULL. |

## Return Value

(int) Returns non-zero on success, zero on failure. Use
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to obtain the specific
error.

## Remarks

Set a new write dir. This will override the previous setting.

All attempts to open a file for writing via PhysicsFS will fail until there
is a valid write dir specified through this function.

This call will fail (and fail to change the write dir) if the current write
dir still has files open in it.

Passing a NULL here disables the write dir, so no files can be opened for
writing via PhysicsFS, until a later call specifies a new write dir.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_getWriteDir](PHYSFS_getWriteDir)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

