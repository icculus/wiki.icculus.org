# PHYSFS_writeULE32

Convert and write an unsigned 32-bit littleendian value.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_writeULE32(PHYSFS_File *file, PHYSFS_uint32 val);
```

## Function Parameters

|                                |          |                                          |
| ------------------------------ | -------- | ---------------------------------------- |
| [PHYSFS_File](PHYSFS_File) *   | **file** | PhysicsFS file handle to which to write. |
| [PHYSFS_uint32](PHYSFS_uint32) | **val**  | Value to convert and write.              |

## Return Value

(int) Returns zero on failure, non-zero on success. On failure, you can
find out what went wrong from
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)().

## Remarks

Convenience function. Convert an unsigned 32-bit value from the platform's
native byte order to littleendian and write it to a file.

## Thread Safety

Multiple threads can not operate on the same [PHYSFS_File](PHYSFS_File) at
the same time, but they can safely operate on _different_ ones
simultaneously.

## Version

This function is available since PhysicsFS 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

