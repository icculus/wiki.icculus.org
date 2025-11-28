# PHYSFS_mountHandle

Add an archive, contained in a [PHYSFS_File](PHYSFS_File) handle, to the search path.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_mountHandle(PHYSFS_File *file, const char *newDir,
    const char *mountPoint, int appendToPath);
```

## Function Parameters

|                              |                  |                                                                                                                                           |
| ---------------------------- | ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| [PHYSFS_File](PHYSFS_File) * | **file**         | The [PHYSFS_File](PHYSFS_File) handle containing archive data.                                                                            |
| const char *                 | **newDir**       | Filename that can represent this stream.                                                                                                  |
| const char *                 | **mountPoint**   | Location in the interpolated tree that this archive will be "mounted", in platform-independent notation. NULL or "" is equivalent to "/". |
| int                          | **appendToPath** | nonzero to append to search path, zero to prepend.                                                                                        |

## Return Value

(int) Returns nonzero if added to path, zero on failure (bogus archive,
etc). Use [PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to obtain
the specific error.

## Remarks

**WARNING**: Unless you have some special, low-level need, you should be
using [PHYSFS_mount](PHYSFS_mount)() instead of this.

**WARNING**: Archives-in-archives may be very slow! While a
[PHYSFS_File](PHYSFS_File) can seek even when the data is compressed, it
may do so by rewinding to the start and decompressing everything before the
seek point. Normal archive usage may do a lot of seeking behind the scenes.
As such, you might find normal archive usage extremely painful if mounted
this way. Plan accordingly: if you, say, have a self-extracting .zip file,
and want to mount something in it, compress the contents of the inner
archive and make sure the outer .zip file doesn't compress the inner
archive too.

This function operates just like [PHYSFS_mount](PHYSFS_mount)(), but takes
a [PHYSFS_File](PHYSFS_File) handle instead of a pathname. This handle
contains all the data of the archive, and is used instead of a real file in
the physical filesystem. The [PHYSFS_File](PHYSFS_File) may be backed by a
real file in the physical filesystem, but isn't necessarily. The most
popular use for this is likely to mount archives stored inside other
archives.

`newDir` must be a unique string to identify this archive. It is used to
optimize archiver selection (if you name it XXXXX.zip, we might try the ZIP
archiver first, for example, or directly choose an archiver that can only
trust the data is valid by filename extension). It doesn't need to refer to
a real file at all. If the filename extension isn't helpful, the system
will try every archiver until one works or none of them do. This filename
must be unique, as the system won't allow you to have two archives with the
same name.

`file` must remain until the archive is unmounted. When the archive is
unmounted, the system will call [PHYSFS_close](PHYSFS_close)(file). If you
need this handle to survive, you will have to wrap this in a
[PHYSFS_Io](PHYSFS_Io) and use [PHYSFS_mountIo](PHYSFS_mountIo)() instead.

If this function fails, [PHYSFS_close](PHYSFS_close)(file) is not called.

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

