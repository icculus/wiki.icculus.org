# PHYSFS_utf8FromUcs4

Convert a UCS-4 string to a UTF-8 string.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
void PHYSFS_utf8FromUcs4(const PHYSFS_uint32 *src, char *dst, PHYSFS_uint64 len);
```

## Function Parameters

|                                        |         |                                                |
| -------------------------------------- | ------- | ---------------------------------------------- |
| const [PHYSFS_uint32](PHYSFS_uint32) * | **src** | Null-terminated source string in UCS-4 format. |
| char *                                 | **dst** | Buffer to store converted UTF-8 string.        |
| [PHYSFS_uint64](PHYSFS_uint64)         | **len** | Size, in bytes, of destination buffer.         |

## Remarks

**WARNING**: This function will not report an error if there are invalid
UCS-4 values in the source string. It will replace them with a '?'
character and continue on.

UCS-4 (aka UTF-32) strings are 32-bits per character: \c wchar_t on Unix.

To ensure that the destination buffer is large enough for the conversion,
please allocate a buffer that is the same size as the source buffer. UTF-8
never uses more than 32-bits per character, so while it may shrink a UCS-4
string, it will never expand it.

Strings that don't fit in the destination buffer will be truncated, but
will always be null-terminated and never have an incomplete UTF-8 sequence
at the end. If the buffer length is 0, this function does nothing.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

