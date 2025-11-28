# PHYSFS_deregisterArchiver

Remove an archiver from the system.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_deregisterArchiver(const char *ext);
```

## Function Parameters

|              |         |                                               |
| ------------ | ------- | --------------------------------------------- |
| const char * | **ext** | Filename extension that the archiver handles. |

## Return Value

(int) Returns Zero on error, non-zero on success.

## Remarks

If for some reason, you only need your previously-registered archiver to
live for a portion of your app's lifetime, you can remove it from the
system once you're done with it through this function.

This fails if there are any archives still open that use this archiver.

This function can also remove internally-supplied archivers, like .zip
support or whatnot. This could be useful in some situations, like disabling
support for them outright or overriding them with your own implementation.
Once an internal archiver is disabled like this, PhysicsFS provides no
mechanism to recover them, short of calling
[PHYSFS_deinit](PHYSFS_deinit)() and [PHYSFS_init](PHYSFS_init)() again.

[PHYSFS_deinit](PHYSFS_deinit)() will automatically deregister all
archivers, so you don't need to explicitly deregister yours if you
otherwise shut down cleanly.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_Archiver](PHYSFS_Archiver)
- [PHYSFS_registerArchiver](PHYSFS_registerArchiver)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

