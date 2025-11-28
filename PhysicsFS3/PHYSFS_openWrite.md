# PHYSFS_openWrite

Open a file for writing.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
PHYSFS_File * PHYSFS_openWrite(const char *filename);
```

## Function Parameters

|              |              |               |
| ------------ | ------------ | ------------- |
| const char * | **filename** | File to open. |

## Return Value

([PHYSFS_File](PHYSFS_File) *) Returns A valid PhysicsFS filehandle on
success, NULL on error. Use
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to obtain the specific
error.

## Remarks

Open a file for writing, in platform-independent notation and in relation
to the write dir as the root of the writable filesystem. The specified file
is created if it doesn't exist. If it does exist, it is truncated to zero
bytes, and the writing offset is set to the start.

Note that entries that are symlinks are ignored if
[PHYSFS_permitSymbolicLinks](PHYSFS_permitSymbolicLinks)(1) hasn't been
called, and opening a symlink with this function will fail in such a case.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_openRead](PHYSFS_openRead)
- [PHYSFS_openAppend](PHYSFS_openAppend)
- [PHYSFS_write](PHYSFS_write)
- [PHYSFS_close](PHYSFS_close)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

