# PHYSFS_enumerateFilesCallback

Get a file listing of a search path's directory, using an application-defined callback.

## Deprecated

As of PhysicsFS 2.1, use [PHYSFS_enumerate](PHYSFS_enumerate)() instead.
This function has no way to report errors (or to have the callback signal
an error or request a stop), so if data will be lost, your callback has no
way to direct the process, and your calling app has no way to know.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
void PHYSFS_enumerateFilesCallback(const char *dir,
                                               PHYSFS_EnumFilesCallback c,
                                               void *d);
```

## Remarks

As of PhysicsFS 2.1, this function just wraps
[PHYSFS_enumerate](PHYSFS_enumerate)() and ignores errors. Consider using
[PHYSFS_enumerate](PHYSFS_enumerate)() or
[PHYSFS_enumerateFiles](PHYSFS_enumerateFiles)() instead.

## Thread Safety

It is safe to call this function from any thread, but this function will
hold a lock that prevents many other PhysicsFS functions from running until
your callback returns and this function finishes. This is only a problem if
you're using this callback to farm work off to other threads that will want
to use PhysicsFS to do work (like enumerating files that another thread
reads in and processes).

## Version

This function is available since PhysicsFS 2.0.0.

## See Also

- [PHYSFS_enumerate](PHYSFS_enumerate)
- [PHYSFS_enumerateFiles](PHYSFS_enumerateFiles)
- [PHYSFS_EnumFilesCallback](PHYSFS_EnumFilesCallback)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

