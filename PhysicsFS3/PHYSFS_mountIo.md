# PHYSFS_mountIo

Add an archive, built on a [PHYSFS_Io](PHYSFS_Io), to the search path.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_mountIo(PHYSFS_Io *io,
 const char *newDir, const char *mountPoint,
 int appendToPath);
```

## Function Parameters

|                          |                  |                                                                                                                                           |
| ------------------------ | ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| [PHYSFS_Io](PHYSFS_Io) * | **io**           | i/o instance for archive to add to the path.                                                                                              |
| const char *             | **newDir**       | Filename that can represent this stream.                                                                                                  |
| const char *             | **mountPoint**   | Location in the interpolated tree that this archive will be "mounted", in platform-independent notation. NULL or "" is equivalent to "/". |
| int                      | **appendToPath** | nonzero to append to search path, zero to prepend.                                                                                        |

## Return Value

(int) Returns nonzero if added to path, zero on failure (bogus archive,
stream i/o issue, etc). Use
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to obtain the specific
error.

## Remarks

**WARNING**: Unless you have some special, low-level need, you should be
using [PHYSFS_mount](PHYSFS_mount)() instead of this.

This function operates just like [PHYSFS_mount](PHYSFS_mount)(), but takes
a [PHYSFS_Io](PHYSFS_Io) instead of a pathname. Behind the scenes,
[PHYSFS_mount](PHYSFS_mount)() calls this function with a
physical-filesystem-based [PHYSFS_Io](PHYSFS_Io).

`newDir` must be a unique string to identify this archive. It is used to
optimize archiver selection (if you name it XXXXX.zip, we might try the ZIP
archiver first, for example, or directly choose an archiver that can only
trust the data is valid by filename extension). It doesn't need to refer to
a real file at all. If the filename extension isn't helpful, the system
will try every archiver until one works or none of them do. This filename
must be unique, as the system won't allow you to have two archives with the
same name.

`io` must remain until the archive is unmounted. When the archive is
unmounted, the system will call `io->destroy(io)`, which will give you a
chance to free your resources.

If this function fails, `io->destroy(io)` is not called.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_unmount](PHYSFS_unmount)
- [PHYSFS_getSearchPath](PHYSFS_getSearchPath)
- [PHYSFS_getMountPoint](PHYSFS_getMountPoint)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

