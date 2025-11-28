# PHYSFS_setRoot

Make a subdirectory of an archive its root directory.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_setRoot(const char *archive, const char *subdir);
```

## Function Parameters

|              |             |                                                    |
| ------------ | ----------- | -------------------------------------------------- |
| const char * | **archive** | dir/archive on which to change root.               |
| const char * | **subdir**  | new subdirectory to make the root of this archive. |

## Return Value

(int) Returns nonzero on success, zero on failure. Use
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to obtain the specific
error.

## Remarks

This lets you narrow down the accessible files in a specific archive. For
example, if you have x.zip with a file in y/z.txt, mounted to /a, if you
call [PHYSFS_setRoot](PHYSFS_setRoot)("x.zip", "/y"), then the call
[PHYSFS_openRead](PHYSFS_openRead)("/a/z.txt") will succeed.

You can change an archive's root at any time, altering the interpolated
file tree (depending on where paths shift, a different archive may be
providing various files). If you set the root to NULL or "/", the archive
will be treated as if no special root was set (as if the archive was just
mounted normally).

Changing the root only affects future operations on pathnames; a file that
was opened from a path that changed due to a setRoot will not be affected.

Setting a new root is not limited to archives in the search path; you may
set one on the write dir, too, which might be useful if you have files open
for write and thus can't change the write dir at the moment.

It is not an error to set a subdirectory that does not exist to be the root
of an archive; however, no files will be visible in this case. If the
missing directories end up getting created (a mkdir to the physical
filesystem, etc) then this will be reflected in the interpolated tree.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 3.1.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

