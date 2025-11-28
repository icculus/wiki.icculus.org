# PHYSFS_getLastModTime

Get the last modification time of a file.

## Deprecated

As of PhysicsFS 2.1, use [PHYSFS_stat](PHYSFS_stat)() instead. This
function just wraps it anyhow.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
PHYSFS_sint64 PHYSFS_getLastModTime(const char *filename);
```

## Function Parameters

|              |              |                                                      |
| ------------ | ------------ | ---------------------------------------------------- |
| const char * | **filename** | filename to check, in platform-independent notation. |

## Return Value

([PHYSFS_sint64](PHYSFS_sint64)) Returns last modified time of the file. -1
if it can't be determined.

## Remarks

The modtime is returned as a number of seconds since the Unix epoch
(midnight, Jan 1, 1970). The exact derivation and accuracy of this time
depends on the particular archiver. If there is no reasonable way to obtain
this information for a particular archiver, or there was some sort of
error, this function returns (-1).

You must use this and not [PHYSFS_stat](PHYSFS_stat)() if binary
compatibility with PhysicsFS 2.0 is important (which it may not be for many
people).

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_stat](PHYSFS_stat)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

