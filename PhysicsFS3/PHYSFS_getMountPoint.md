# PHYSFS_getMountPoint

Determine a mounted archive's mountpoint.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
const char * PHYSFS_getMountPoint(const char *dir);
```

## Function Parameters

|              |         |                                                                                                                                                                                                                               |
| ------------ | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| const char * | **dir** | directory or archive previously added to the path, in platform-dependent notation. This must match the string used when adding, even if your string would also reference the same file with a different string of characters. |

## Return Value

(const char *) Returns READ-ONLY string of mount point if added to path,
NULL on failure (bogus archive, etc). Use
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to obtain the specific
error.

## Remarks

You give this function the name of an archive or dir you successfully added
to the search path, and it reports the location in the interpolated tree
where it is mounted. Files mounted with a NULL mountpoint or through
[PHYSFS_addToSearchPath](PHYSFS_addToSearchPath)() will report "/". The
return value is READ ONLY and valid until the archive is removed from the
search path.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.0.0.

## See Also

- [PHYSFS_removeFromSearchPath](PHYSFS_removeFromSearchPath)
- [PHYSFS_getSearchPath](PHYSFS_getSearchPath)
- [PHYSFS_getMountPoint](PHYSFS_getMountPoint)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

