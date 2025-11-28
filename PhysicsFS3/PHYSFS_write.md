# PHYSFS_write

Write data to a PhysicsFS filehandle.

## Deprecated

As of PhysicsFS 2.1, use [PHYSFS_writeBytes](PHYSFS_writeBytes)() instead.
This function just wraps it anyhow. This function never clarified what
would happen if you managed to write a partial object, so working at the
byte level makes this cleaner for everyone, especially now that
[PHYSFS_Io](PHYSFS_Io) interfaces can be supplied by the application.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
PHYSFS_sint64 PHYSFS_write(PHYSFS_File *handle,
                                       const void *buffer,
                                       PHYSFS_uint32 objSize,
                                       PHYSFS_uint32 objCount);
```

## Function Parameters

|                                |              |                                                                                                 |
| ------------------------------ | ------------ | ----------------------------------------------------------------------------------------------- |
| [PHYSFS_File](PHYSFS_File) *   | **handle**   | retval from [PHYSFS_openWrite](PHYSFS_openWrite)() or [PHYSFS_openAppend](PHYSFS_openAppend)(). |
| const void *                   | **buffer**   | buffer of bytes to write to `handle`.                                                           |
| [PHYSFS_uint32](PHYSFS_uint32) | **objSize**  | size in bytes of objects being written to `handle`.                                             |
| [PHYSFS_uint32](PHYSFS_uint32) | **objCount** | number of `objSize` objects to write to `handle`.                                               |

## Return Value

([PHYSFS_sint64](PHYSFS_sint64)) Returns number of objects written.
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() can shed light on the
reason this might be < `objCount`. -1 if complete failure.

## Remarks

The file must be opened for writing.

## Thread Safety

Multiple threads can not operate on the same [PHYSFS_File](PHYSFS_File) at
the same time, but they can safely operate on _different_ ones
simultaneously.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_writeBytes](PHYSFS_writeBytes)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

