# PHYSFS_symbolicLinksPermitted

Determine if the symbolic links are permitted.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_symbolicLinksPermitted(void);
```

## Return Value

(int) Returns non-zero if symlinks are permitted, zero if not.

## Remarks

This reports the setting from the last call to
[PHYSFS_permitSymbolicLinks](PHYSFS_permitSymbolicLinks)(). If
[PHYSFS_permitSymbolicLinks](PHYSFS_permitSymbolicLinks)() hasn't been
called since the library was last initialized, symbolic links are
implicitly disabled.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.0.0.

## See Also

- [PHYSFS_permitSymbolicLinks](PHYSFS_permitSymbolicLinks)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

