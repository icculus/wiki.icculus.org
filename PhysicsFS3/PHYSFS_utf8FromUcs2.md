# PHYSFS_utf8FromUcs2

Convert a UCS-2 string to a UTF-8 string.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
void PHYSFS_utf8FromUcs2(const PHYSFS_uint16 *src, char *dst,
      PHYSFS_uint64 len);
```

## Function Parameters

|                                        |         |                                                |
| -------------------------------------- | ------- | ---------------------------------------------- |
| const [PHYSFS_uint16](PHYSFS_uint16) * | **src** | Null-terminated source string in UCS-2 format. |
| char *                                 | **dst** | Buffer to store converted UTF-8 string.        |
| [PHYSFS_uint64](PHYSFS_uint64)         | **len** | Size, in bytes, of destination buffer.         |

## Remarks

**WARNING**: you almost certainly should use
[PHYSFS_utf8FromUtf16](PHYSFS_utf8FromUtf16)(), which became available in
PhysicsFS 2.1, unless you know what you're doing.

**WARNING**: This function will not report an error if there are invalid
UCS-2 values in the source string. It will replace them with a '?'
character and continue on.

UCS-2 strings are 16-bits per character: \c TCHAR on Windows, when building
with Unicode support. Please note that modern versions of Windows use
UTF-16, which is an extended form of UCS-2, and not UCS-2 itself. You
almost certainly want [PHYSFS_utf8FromUtf16](PHYSFS_utf8FromUtf16)()
instead.

To ensure that the destination buffer is large enough for the conversion,
please allocate a buffer that is double the size of the source buffer.
UTF-8 never uses more than 32-bits per character, so while it may shrink a
UCS-2 string, it may also expand it.

Strings that don't fit in the destination buffer will be truncated, but
will always be null-terminated and never have an incomplete UTF-8 sequence
at the end. If the buffer length is 0, this function does nothing.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.0.0.

## See Also

- [PHYSFS_utf8FromUtf16](PHYSFS_utf8FromUtf16)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

