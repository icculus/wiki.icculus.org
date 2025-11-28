# PHYSFS_openRead

Open a file for reading.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
PHYSFS_File * PHYSFS_openRead(const char *filename);
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

Open a file for reading, in platform-independent notation. The search path
is checked one at a time until a matching file is found, in which case an
abstract filehandle is associated with it, and reading may be done. The
reading offset is set to the first byte of the file.

Note that entries that are symlinks are ignored if
[PHYSFS_permitSymbolicLinks](PHYSFS_permitSymbolicLinks)(1) hasn't been
called, and opening a symlink with this function will fail in such a case.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_openWrite](PHYSFS_openWrite)
- [PHYSFS_openAppend](PHYSFS_openAppend)
- [PHYSFS_read](PHYSFS_read)
- [PHYSFS_close](PHYSFS_close)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

