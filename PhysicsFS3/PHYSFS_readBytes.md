# PHYSFS_readBytes

Read bytes from a PhysicsFS filehandle.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
PHYSFS_sint64 PHYSFS_readBytes(PHYSFS_File *handle, void *buffer, PHYSFS_uint64 len);
```

## Function Parameters

|                                |            |                                                            |
| ------------------------------ | ---------- | ---------------------------------------------------------- |
| [PHYSFS_File](PHYSFS_File) *   | **handle** | handle returned from [PHYSFS_openRead](PHYSFS_openRead)(). |
| void *                         | **buffer** | buffer of at least `len` bytes to store read data into.    |
| [PHYSFS_uint64](PHYSFS_uint64) | **len**    | number of bytes being read from `handle`.                  |

## Return Value

([PHYSFS_sint64](PHYSFS_sint64)) Returns number of bytes read. This may be
less than `len`; this does not signify an error, necessarily (a short read
may mean EOF). [PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() can
shed light on the reason this might be < `len`, as can
[PHYSFS_eof](PHYSFS_eof)(). -1 if complete failure.

## Remarks

The file must be opened for reading.

## Thread Safety

Multiple threads can not operate on the same [PHYSFS_File](PHYSFS_File) at
the same time, but they can safely operate on _different_ ones
simultaneously.

## Version

This function is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_eof](PHYSFS_eof)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

