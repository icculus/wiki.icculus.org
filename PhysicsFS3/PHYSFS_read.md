# PHYSFS_read

Read data from a PhysicsFS filehandle.

## Deprecated

As of PhysicsFS 2.1, use [PHYSFS_readBytes](PHYSFS_readBytes)() instead.
This function just wraps it anyhow. This function never clarified what
would happen if you managed to read a partial object, so working at the
byte level makes this cleaner for everyone, especially now that
[PHYSFS_Io](PHYSFS_Io) interfaces can be supplied by the application.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
PHYSFS_sint64 PHYSFS_read(PHYSFS_File *handle,
                                      void *buffer,
                                      PHYSFS_uint32 objSize,
                                      PHYSFS_uint32 objCount);
```

## Function Parameters

|                                |              |                                                            |
| ------------------------------ | ------------ | ---------------------------------------------------------- |
| [PHYSFS_File](PHYSFS_File) *   | **handle**   | handle returned from [PHYSFS_openRead](PHYSFS_openRead)(). |
| void *                         | **buffer**   | buffer to store read data into.                            |
| [PHYSFS_uint32](PHYSFS_uint32) | **objSize**  | size in bytes of objects being read from `handle`.         |
| [PHYSFS_uint32](PHYSFS_uint32) | **objCount** | number of `objSize` objects to read from `handle`.         |

## Return Value

([PHYSFS_sint64](PHYSFS_sint64)) Returns number of objects read.
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() can shed light on the
reason this might be < (objCount), as can [PHYSFS_eof](PHYSFS_eof)(). -1 if
complete failure.

## Remarks

The file must be opened for reading.

## Thread Safety

Multiple threads can not operate on the same [PHYSFS_File](PHYSFS_File) at
the same time, but they can safely operate on _different_ ones
simultaneously.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_readBytes](PHYSFS_readBytes)
- [PHYSFS_eof](PHYSFS_eof)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

