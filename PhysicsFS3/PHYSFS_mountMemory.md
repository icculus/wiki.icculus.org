# PHYSFS_mountMemory

Add an archive, contained in a memory buffer, to the search path.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_mountMemory(const void *buf, PHYSFS_uint64 len,
         PHYSFS_FreeCallback del, const char *newDir,
         const char *mountPoint, int appendToPath);
```

## Function Parameters

|                                            |                  |                                                                                                                                           |
| ------------------------------------------ | ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| const void *                               | **buf**          | Address of the memory buffer containing the archive data.                                                                                 |
| [PHYSFS_uint64](PHYSFS_uint64)             | **len**          | Size of memory buffer, in bytes.                                                                                                          |
| [PHYSFS_FreeCallback](PHYSFS_FreeCallback) | **del**          | A callback that triggers upon unmount. Can be NULL.                                                                                       |
| const char *                               | **newDir**       | Filename that can represent this stream.                                                                                                  |
| const char *                               | **mountPoint**   | Location in the interpolated tree that this archive will be "mounted", in platform-independent notation. NULL or "" is equivalent to "/". |
| int                                        | **appendToPath** | nonzero to append to search path, zero to prepend.                                                                                        |

## Return Value

(int) Returns nonzero if added to path, zero on failure (bogus archive,
etc). Use [PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to obtain
the specific error.

## Remarks

**WARNING**: Unless you have some special, low-level need, you should be
using [PHYSFS_mount](PHYSFS_mount)() instead of this.

This function operates just like [PHYSFS_mount](PHYSFS_mount)(), but takes
a memory buffer instead of a pathname. This buffer contains all the data of
the archive, and is used instead of a real file in the physical filesystem.

`newDir` must be a unique string to identify this archive. It is used to
optimize archiver selection (if you name it XXXXX.zip, we might try the ZIP
archiver first, for example, or directly choose an archiver that can only
trust the data is valid by filename extension). It doesn't need to refer to
a real file at all. If the filename extension isn't helpful, the system
will try every archiver until one works or none of them do. This filename
must be unique, as the system won't allow you to have two archives with the
same name.

`ptr` must remain until the archive is unmounted. When the archive is
unmounted, the system will call `del(ptr)`, which will notify you that the
system is done with the buffer, and give you a chance to free your
resources. `del` can be NULL, in which case the system will make no attempt
to free the buffer.

If this function fails, `del` is not called.

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

