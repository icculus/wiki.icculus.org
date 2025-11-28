# PHYSFS_utf8stricmp

Case-insensitive compare of two UTF-8 strings.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_utf8stricmp(const char *str1, const char *str2);
```

## Function Parameters

|              |          |                           |
| ------------ | -------- | ------------------------- |
| const char * | **str1** | First string to compare.  |
| const char * | **str2** | Second string to compare. |

## Return Value

(int) Returns -1 if str1 is "less than" str2, 1 if "greater than", 0 if
equal.

## Remarks

This is a strcasecmp/stricmp replacement that expects both strings to be in
UTF-8 encoding. It will do "case folding" to decide if the Unicode
codepoints in the strings match.

If both strings are exclusively low-ASCII characters, this will do the
right thing, as that is also valid UTF-8. If there are any high-ASCII
chars, this will not do what you expect!

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

