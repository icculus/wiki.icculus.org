# PHYSFS_getDirSeparator

Get platform-dependent dir separator string.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
const char * PHYSFS_getDirSeparator(void);
```

## Return Value

(const char *) Returns READ ONLY null-terminated string of platform's dir
separator.

## Remarks

This returns "\\" on win32, "/" on Unix, and ":" on MacOS. It may be more
than one character, depending on the platform, and your code should take
that into account. Note that this is only useful for setting up the
search/write paths, since access into those dirs always use '/'
(platform-independent notation) to separate directories. This is also handy
for getting platform-independent access when using stdio calls.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

