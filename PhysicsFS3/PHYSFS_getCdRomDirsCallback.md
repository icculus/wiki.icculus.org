# PHYSFS_getCdRomDirsCallback

Enumerate CD-ROM directories, using an application-defined callback.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
void PHYSFS_getCdRomDirsCallback(PHYSFS_StringCallback c, void *d);
```

## Function Parameters

|                                                |       |                                                           |
| ---------------------------------------------- | ----- | --------------------------------------------------------- |
| [PHYSFS_StringCallback](PHYSFS_StringCallback) | **c** | Callback function to notify about detected drives.        |
| void *                                         | **d** | Application-defined data passed to callback. Can be NULL. |

## Remarks

Internally, [PHYSFS_getCdRomDirs](PHYSFS_getCdRomDirs)() just calls this
function and then builds a list before returning to the application, so
functionality is identical except for how the information is represented to
the application.

Unlike [PHYSFS_getCdRomDirs](PHYSFS_getCdRomDirs)(), this function does not
return an array. Rather, it calls a function specified by the application
once per detected disc:

```c
static void foundDisc(void *data, const char *cddir) {
    printf("cdrom dir [%s] is available.\n", cddir);
}

// ...
PHYSFS_getCdRomDirsCallback(foundDisc, NULL);
```

This call may block while drives spin up. Be forewarned.

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

- [PHYSFS_StringCallback](PHYSFS_StringCallback)
- [PHYSFS_getCdRomDirs](PHYSFS_getCdRomDirs)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

