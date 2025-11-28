# PHYSFS_registerArchiver

Add a new archiver to the system.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_registerArchiver(const PHYSFS_Archiver *archiver);
```

## Function Parameters

|                                            |              |                           |
| ------------------------------------------ | ------------ | ------------------------- |
| const [PHYSFS_Archiver](PHYSFS_Archiver) * | **archiver** | The archiver to register. |

## Return Value

(int) Returns Zero on error, non-zero on success.

## Remarks

**WARNING**: This is advanced, hardcore stuff. You don't need this unless
you really know what you're doing. Most apps will not need this.

If you want to provide your own archiver (for example, a custom archive
file format, or some virtual thing you want to make look like a filesystem
that you can access through the usual PhysicsFS APIs), this is where you
start. Once an archiver is successfully registered, then you can use
[PHYSFS_mount](PHYSFS_mount)() to add archives that your archiver supports
to the search path, or perhaps use it as the write dir. Internally,
PhysicsFS uses this function to register its own built-in archivers, like
.zip support, etc.

You may not have two archivers that handle the same extension. If you are
going to have a clash, you can deregister the other archiver (including
built-in ones) with
[PHYSFS_deregisterArchiver](PHYSFS_deregisterArchiver)().

The data in (archiver) is copied; you may free this pointer when this
function returns.

Once this function returns successfully, PhysicsFS will be able to support
archives of this type until you deregister the archiver again.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_Archiver](PHYSFS_Archiver)
- [PHYSFS_deregisterArchiver](PHYSFS_deregisterArchiver)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

