# PHYSFS_tell

Determine current position within a PhysicsFS filehandle.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
PHYSFS_sint64 PHYSFS_tell(PHYSFS_File *handle);
```

## Function Parameters

|                              |            |                                                     |
| ---------------------------- | ---------- | --------------------------------------------------- |
| [PHYSFS_File](PHYSFS_File) * | **handle** | handle returned from [PHYSFS_open](PHYSFS_open)*(). |

## Return Value

([PHYSFS_sint64](PHYSFS_sint64)) Returns offset in bytes from start of
file. -1 if error occurred. Use
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to obtain the specific
error.

## Thread Safety

Multiple threads can not operate on the same [PHYSFS_File](PHYSFS_File) at
the same time, but they can safely operate on _different_ ones
simultaneously.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_seek](PHYSFS_seek)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

