# PHYSFS_utf16stricmp

Case-insensitive compare of two UTF-16 strings.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_utf16stricmp(const PHYSFS_uint16 *str1,
     const PHYSFS_uint16 *str2);
```

## Function Parameters

|                                        |          |                           |
| -------------------------------------- | -------- | ------------------------- |
| const [PHYSFS_uint16](PHYSFS_uint16) * | **str1** | First string to compare.  |
| const [PHYSFS_uint16](PHYSFS_uint16) * | **str2** | Second string to compare. |

## Return Value

(int) Returns -1 if str1 is "less than" str2, 1 if "greater than", 0 if
equal.

## Remarks

This is a strcasecmp/stricmp replacement that expects both strings to be in
UTF-16 encoding. It will do "case folding" to decide if the Unicode
codepoints in the strings match.

It will report which string is "greater than" the other, but be aware that
this doesn't necessarily mean anything: 'a' may be "less than" 'b', but a
Japanese kuten has no meaningful alphabetically relationship to a Greek
lambda, but being able to assign a reliable "value" makes sorting
algorithms possible, if not entirely sane. Most cases should treat the
return value as "equal" or "not equal".

Like stricmp, this expects both strings to be NULL-terminated.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.1.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

