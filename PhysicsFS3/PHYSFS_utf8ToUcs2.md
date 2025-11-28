# PHYSFS_utf8ToUcs2

Convert a UTF-8 string to a UCS-2 string.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
void PHYSFS_utf8ToUcs2(const char *src, PHYSFS_uint16 *dst, PHYSFS_uint64 len);
```

## Function Parameters

|                                  |         |                                                |
| -------------------------------- | ------- | ---------------------------------------------- |
| const char *                     | **src** | Null-terminated source string in UTF-8 format. |
| [PHYSFS_uint16](PHYSFS_uint16) * | **dst** | Buffer to store converted UCS-2 string.        |
| [PHYSFS_uint64](PHYSFS_uint64)   | **len** | Size, in bytes, of destination buffer.         |

## Remarks

**WARNING**: you almost certainly should use
[PHYSFS_utf8ToUtf16](PHYSFS_utf8ToUtf16)(), which became available in
PhysicsFS 2.1, unless you know what you're doing.

**WARNING**: This function will not report an error if there are invalid
UTF-8 sequences in the source string. It will replace them with a '?'
character and continue on.

UCS-2 strings are 16-bits per character: \c TCHAR on Windows, when building
with Unicode support. Please note that modern versions of Windows use
UTF-16, which is an extended form of UCS-2, and not UCS-2 itself. You
almost certainly want [PHYSFS_utf8ToUtf16](PHYSFS_utf8ToUtf16)() instead,
but you need to understand how that changes things, too.

To ensure that the destination buffer is large enough for the conversion,
please allocate a buffer that is double the size of the source buffer.
UTF-8 uses from one to four bytes per character, but UCS-2 always uses two,
so an entirely low-ASCII string will double in size!

Strings that don't fit in the destination buffer will be truncated, but
will always be null-terminated and never have an incomplete UCS-2 sequence
at the end. If the buffer length is 0, this function does nothing.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.0.0.

## See Also

- [PHYSFS_utf8ToUtf16](PHYSFS_utf8ToUtf16)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

