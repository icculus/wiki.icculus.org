# PHYSFS_writeBytes

Write data to a PhysicsFS filehandle.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
PHYSFS_sint64 PHYSFS_writeBytes(PHYSFS_File *handle, const void *buffer, PHYSFS_uint64 len);
```

## Function Parameters

|                                |            |                                                                                                 |
| ------------------------------ | ---------- | ----------------------------------------------------------------------------------------------- |
| [PHYSFS_File](PHYSFS_File) *   | **handle** | retval from [PHYSFS_openWrite](PHYSFS_openWrite)() or [PHYSFS_openAppend](PHYSFS_openAppend)(). |
| const void *                   | **buffer** | buffer of `len` bytes to write to `handle`.                                                     |
| [PHYSFS_uint64](PHYSFS_uint64) | **len**    | number of bytes being written to `handle`.                                                      |

## Return Value

([PHYSFS_sint64](PHYSFS_sint64)) Returns number of bytes written. This may
be less than `len`; in the case of an error, the system may try to write as
many bytes as possible, so an incomplete write might occur.
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() can shed light on the
reason this might be < `len`. -1 if complete failure.

## Remarks

The file must be opened for writing.

Please note that while `len` is an unsigned 64-bit integer, you are limited
to 63 bits (9223372036854775807 bytes), so we can return a negative value
on error. If length is greater than 0x7FFFFFFFFFFFFFFF, this function will
immediately fail. For systems without a 64-bit datatype, you are limited to
31 bits (0x7FFFFFFF, or 2147483647 bytes). We trust most things won't need
to do multiple gigabytes of i/o in one call anyhow, but why limit things?

## Thread Safety

Multiple threads can not operate on the same [PHYSFS_File](PHYSFS_File) at
the same time, but they can safely operate on _different_ ones
simultaneously.

## Version

This function is available since PhysicsFS 2.1.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

