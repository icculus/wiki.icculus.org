# PHYSFS_seek

Seek to a new position within a PhysicsFS filehandle.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_seek(PHYSFS_File *handle, PHYSFS_uint64 pos);
```

## Function Parameters

|                                |            |                                                     |
| ------------------------------ | ---------- | --------------------------------------------------- |
| [PHYSFS_File](PHYSFS_File) *   | **handle** | handle returned from [PHYSFS_open](PHYSFS_open)*(). |
| [PHYSFS_uint64](PHYSFS_uint64) | **pos**    | number of bytes from start of file to seek to.      |

## Return Value

(int) Returns nonzero on success, zero on error. Use
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to obtain the specific
error.

## Remarks

The next read or write will occur at that place. Seeking past the beginning
or end of the file is not allowed, and causes an error.

## Thread Safety

Multiple threads can not operate on the same [PHYSFS_File](PHYSFS_File) at
the same time, but they can safely operate on _different_ ones
simultaneously.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_tell](PHYSFS_tell)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

