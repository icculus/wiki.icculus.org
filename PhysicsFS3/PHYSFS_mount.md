# PHYSFS_mount

Add an archive or directory to the search path.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_mount(const char *newDir,
                             const char *mountPoint,
                             int appendToPath);
```

## Function Parameters

|              |                  |                                                                                                                                           |
| ------------ | ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| const char * | **newDir**       | directory or archive to add to the path, in platform-dependent notation.                                                                  |
| const char * | **mountPoint**   | Location in the interpolated tree that this archive will be "mounted", in platform-independent notation. NULL or "" is equivalent to "/". |
| int          | **appendToPath** | nonzero to append to search path, zero to prepend.                                                                                        |

## Return Value

(int) Returns nonzero if added to path, zero on failure (bogus archive, dir
missing, etc). Use [PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to
obtain the specific error.

## Remarks

If this is a duplicate, the entry is not added again, even though the
function succeeds. You may not add the same archive to two different
mountpoints: duplicate checking is done against the archive and not the
mountpoint.

When you mount an archive, it is added to a virtual file system...all files
in all of the archives are interpolated into a single hierachical file
tree. Two archives mounted at the same place (or an archive with files
overlapping another mountpoint) may have overlapping files: in such a case,
the file earliest in the search path is selected, and the other files are
inaccessible to the application. This allows archives to be used to
override previous revisions; you can use the mounting mechanism to place
archives at a specific point in the file tree and prevent overlap; this is
useful for downloadable mods that might trample over application data or
each other, for example.

The mountpoint does not need to exist prior to mounting, which is different
than those familiar with the Unix concept of "mounting" may expect. As
well, more than one archive can be mounted to the same mountpoint, or
mountpoints and archive contents can overlap...the interpolation mechanism
still functions as usual.

Specifying a symbolic link to an archive or directory is allowed here,
regardless of the state of
[PHYSFS_permitSymbolicLinks](PHYSFS_permitSymbolicLinks)(). That function
only deals with symlinks inside the mounted directory or archive.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.0.0.

## See Also

- [PHYSFS_removeFromSearchPath](PHYSFS_removeFromSearchPath)
- [PHYSFS_getSearchPath](PHYSFS_getSearchPath)
- [PHYSFS_getMountPoint](PHYSFS_getMountPoint)
- [PHYSFS_mountIo](PHYSFS_mountIo)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

