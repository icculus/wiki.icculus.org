# PHYSFS_getErrorByCode

Get human-readable description string for a given error code.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
const char * PHYSFS_getErrorByCode(PHYSFS_ErrorCode code);
```

## Function Parameters

|                                      |          |                                    |
| ------------------------------------ | -------- | ---------------------------------- |
| [PHYSFS_ErrorCode](PHYSFS_ErrorCode) | **code** | Error code to convert to a string. |

## Return Value

(const char *) Returns READ ONLY string of requested error message, NULL if
this is not a valid PhysicsFS error code. Always check for NULL if you
might be looking up an error code that didn't exist in an earlier version
of PhysicsFS.

## Remarks

Get a static string, in UTF-8 format, that represents an English
description of a given error code.

This string is guaranteed to never change (although we may add new strings
for new error codes in later versions of PhysicsFS), so you can use it for
keying a localization dictionary.

It is safe to call this function at anytime, even before
[PHYSFS_init](PHYSFS_init)().

These strings are meant to be passed on directly to the user. Generally,
applications should only concern themselves with whether a given function
failed, but not care about the specifics much.

Do not attempt to free the returned strings; they are read-only and you
don't own their memory pages.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

