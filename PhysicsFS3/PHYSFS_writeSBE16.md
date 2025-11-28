# PHYSFS_writeSBE16

Convert and write a signed 16-bit bigendian value.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_writeSBE16(PHYSFS_File *file, PHYSFS_sint16 val);
```

## Function Parameters

|                                |          |                                          |
| ------------------------------ | -------- | ---------------------------------------- |
| [PHYSFS_File](PHYSFS_File) *   | **file** | PhysicsFS file handle to which to write. |
| [PHYSFS_sint16](PHYSFS_sint16) | **val**  | Value to convert and write.              |

## Return Value

(int) Returns zero on failure, non-zero on success. On failure, you can
find out what went wrong from
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)().

## Remarks

Convenience function. Convert a signed 16-bit value from the platform's
native byte order to bigendian and write it to a file.

## Thread Safety

Multiple threads can not operate on the same [PHYSFS_File](PHYSFS_File) at
the same time, but they can safely operate on _different_ ones
simultaneously.

## Version

This function is available since PhysicsFS 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

