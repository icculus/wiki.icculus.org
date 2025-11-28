# PHYSFS_utf8FromUtf16

Convert a UTF-16 string to a UTF-8 string.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
void PHYSFS_utf8FromUtf16(const PHYSFS_uint16 *src, char *dst, PHYSFS_uint64 len);
```

## Function Parameters

|                                        |         |                                                 |
| -------------------------------------- | ------- | ----------------------------------------------- |
| const [PHYSFS_uint16](PHYSFS_uint16) * | **src** | Null-terminated source string in UTF-16 format. |
| char *                                 | **dst** | Buffer to store converted UTF-8 string.         |
| [PHYSFS_uint64](PHYSFS_uint64)         | **len** | Size, in bytes, of destination buffer.          |

## Remarks

**WARNING**: This function will not report an error if there are invalid
UTF-16 sequences in the source string. It will replace them with a '?'
character and continue on.

UTF-16 strings are 16-bits per character (except some chars, which are
32-bits): \c TCHAR on Windows, when building with Unicode support. Modern
Windows releases use UTF-16. Windows releases before 2000 used TCHAR, but
only handled UCS-2. UTF-16 _is_ UCS-2, except for the characters that are 4
bytes, which aren't representable in UCS-2 at all anyhow. If you aren't
sure, you should be using UTF-16 at this point on Windows.

To ensure that the destination buffer is large enough for the conversion,
please allocate a buffer that is double the size of the source buffer.
UTF-8 never uses more than 32-bits per character, so while it may shrink a
UTF-16 string, it may also expand it.

Strings that don't fit in the destination buffer will be truncated, but
will always be null-terminated and never have an incomplete UTF-8 sequence
at the end. If the buffer length is 0, this function does nothing.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.1.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

