# PHYSFS_utf8ToUcs4

Convert a UTF-8 string to a UCS-4 string.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
void PHYSFS_utf8ToUcs4(const char *src, PHYSFS_uint32 *dst,
    PHYSFS_uint64 len);
```

## Function Parameters

|                                  |         |                                                |
| -------------------------------- | ------- | ---------------------------------------------- |
| const char *                     | **src** | Null-terminated source string in UTF-8 format. |
| [PHYSFS_uint32](PHYSFS_uint32) * | **dst** | Buffer to store converted UCS-4 string.        |
| [PHYSFS_uint64](PHYSFS_uint64)   | **len** | Size, in bytes, of destination buffer.         |

## Remarks

**WARNING**: This function will not report an error if there are invalid
UTF-8 sequences in the source string. It will replace them with a '?'
character and continue on.

UCS-4 (aka UTF-32) strings are 32-bits per character: \c wchar_t on Unix.

To ensure that the destination buffer is large enough for the conversion,
please allocate a buffer that is four times the size of the source buffer.
UTF-8 uses from one to four bytes per character, but UCS-4 always uses
four, so an entirely low-ASCII string will quadruple in size!

Strings that don't fit in the destination buffer will be truncated, but
will always be null-terminated and never have an incomplete UCS-4 sequence
at the end. If the buffer length is 0, this function does nothing.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

