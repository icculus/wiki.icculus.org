# PHYSFS_readSBE64

Read and convert a signed 64-bit bigendian value.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_readSBE64(PHYSFS_File *file, PHYSFS_sint64 *val);
```

## Function Parameters

|                                  |          |                                           |
| -------------------------------- | -------- | ----------------------------------------- |
| [PHYSFS_File](PHYSFS_File) *     | **file** | PhysicsFS file handle from which to read. |
| [PHYSFS_sint64](PHYSFS_sint64) * | **val**  | pointer to where value should be stored.  |

## Return Value

(int) Returns zero on failure, non-zero on success. If successful, `*val`
will store the result. On failure, you can find out what went wrong from
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)().

## Remarks

Convenience function. Read a signed 64-bit bigendian value from a file and
convert it to the platform's native byte order.

**WARNING**: Remember, [PHYSFS_sint64](PHYSFS_sint64) is only 32 bits on
platforms without any sort of 64-bit support.

## Thread Safety

Multiple threads can not operate on the same [PHYSFS_File](PHYSFS_File) at
the same time, but they can safely operate on _different_ ones
simultaneously.

## Version

This function is available since PhysicsFS 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

