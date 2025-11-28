# PHYSFS_permitSymbolicLinks

Enable or disable following of symbolic links.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
void PHYSFS_permitSymbolicLinks(int allow);
```

## Function Parameters

|     |           |                                                   |
| --- | --------- | ------------------------------------------------- |
| int | **allow** | nonzero to permit symlinks, zero to deny linking. |

## Remarks

Some physical filesystems and archives contain files that are just pointers
to other files. On the physical filesystem, opening such a link will
(transparently) open the file that is pointed to.

By default, PhysicsFS will check if a file is really a symlink during open
calls and fail if it is. Otherwise, the link could take you outside the
write and search paths, and compromise security.

If you want to take that risk, call this function with a non-zero
parameter. Note that this is more for sandboxing a program's scripting
language, in case untrusted scripts try to compromise the system. Generally
speaking, a user could very well have a legitimate reason to set up a
symlink, so unless you feel there's a specific danger in allowing them, you
should permit them.

Symlinks are only explicitly checked when dealing with filenames in
platform-independent notation. That is, when setting up your search and
write paths, etc, symlinks are never checked for.

Please note that [PHYSFS_stat](PHYSFS_stat)() will always check the path
specified; if that path is a symlink, it will not be followed in any case.
If symlinks aren't permitted through this function,
[PHYSFS_stat](PHYSFS_stat)() ignores them, and would treat the query as if
the path didn't exist at all.

Symbolic link permission can be enabled or disabled at any time after
you've called [PHYSFS_init](PHYSFS_init)(), and is disabled by default.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_symbolicLinksPermitted](PHYSFS_symbolicLinksPermitted)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

