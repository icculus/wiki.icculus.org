# PHYSFS_utf8FromLatin1

Convert a UTF-8 string to a Latin1 string.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
void PHYSFS_utf8FromLatin1(const char *src, char *dst, PHYSFS_uint64 len);
```

## Function Parameters

|                                |         |                                                 |
| ------------------------------ | ------- | ----------------------------------------------- |
| const char *                   | **src** | Null-terminated source string in Latin1 format. |
| char *                         | **dst** | Buffer to store converted UTF-8 string.         |
| [PHYSFS_uint64](PHYSFS_uint64) | **len** | Size, in bytes, of destination buffer.          |

## Remarks

Latin1 strings are 8-bits per character: a popular "high ASCII" encoding.

To ensure that the destination buffer is large enough for the conversion,
please allocate a buffer that is double the size of the source buffer.
UTF-8 expands latin1 codepoints over 127 from 1 to 2 bytes, so the string
may grow in some cases.

Strings that don't fit in the destination buffer will be truncated, but
will always be null-terminated and never have an incomplete UTF-8 sequence
at the end. If the buffer length is 0, this function does nothing.

Please note that we do not supply a UTF-8 to Latin1 converter, since Latin1
can't express most Unicode codepoints. It's a legacy encoding; you should
be converting away from it at all times.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

