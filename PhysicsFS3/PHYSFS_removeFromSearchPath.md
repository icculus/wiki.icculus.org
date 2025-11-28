# PHYSFS_removeFromSearchPath

Remove a directory or archive from the search path.

## Deprecated

As of PhysicsFS 2.1, use [PHYSFS_unmount](PHYSFS_unmount)() instead. This
function just wraps it anyhow. There's no functional difference except the
vocabulary changed from "adding to the search path" to "mounting" when that
functionality was extended, and thus the preferred way to accomplish this
function's work is now called "unmounting."

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_removeFromSearchPath(const char *oldDir);
```

## Remarks

This function is equivalent to:

```c
PHYSFS_unmount(oldDir);
```

You must use this and not [PHYSFS_unmount](PHYSFS_unmount) if binary
compatibility with PhysicsFS 1.0 is important (which it may not be for many
people).

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_addToSearchPath](PHYSFS_addToSearchPath)
- [PHYSFS_getSearchPath](PHYSFS_getSearchPath)
- [PHYSFS_unmount](PHYSFS_unmount)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

