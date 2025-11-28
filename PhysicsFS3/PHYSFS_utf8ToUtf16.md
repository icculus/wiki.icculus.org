# PHYSFS_utf8ToUtf16

Convert a UTF-8 string to a UTF-16 string.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
void PHYSFS_utf8ToUtf16(const char *src, PHYSFS_uint16 *dst, PHYSFS_uint64 len);
```

## Function Parameters

|                                  |         |                                                |
| -------------------------------- | ------- | ---------------------------------------------- |
| const char *                     | **src** | Null-terminated source string in UTF-8 format. |
| [PHYSFS_uint16](PHYSFS_uint16) * | **dst** | Buffer to store converted UTF-16 string.       |
| [PHYSFS_uint64](PHYSFS_uint64)   | **len** | Size, in bytes, of destination buffer.         |

## Remarks

**WARNING**: This function will not report an error if there are invalid
UTF-8 sequences in the source string. It will replace them with a '?'
character and continue on.

UTF-16 strings are 16-bits per character (except some chars, which are
32-bits): \c TCHAR on Windows, when building with Unicode support. Modern
Windows releases use UTF-16. Windows releases before 2000 used TCHAR, but
only handled UCS-2. UTF-16 _is_ UCS-2, except for the characters that are 4
bytes, which aren't representable in UCS-2 at all anyhow. If you aren't
sure, you should be using UTF-16 at this point on Windows.

To ensure that the destination buffer is large enough for the conversion,
please allocate a buffer that is double the size of the source buffer.
UTF-8 uses from one to four bytes per character, but UTF-16 always uses two
to four, so an entirely low-ASCII string will double in size! The UTF-16
characters that would take four bytes also take four bytes in UTF-8, so you
don't need to allocate 4x the space just in case: double will do.

Strings that don't fit in the destination buffer will be truncated, but
will always be null-terminated and never have an incomplete UTF-16
surrogate pair at the end. If the buffer length is 0, this function does
nothing.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_utf8ToUtf16](PHYSFS_utf8ToUtf16)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

