# PHYSFS_getBaseDir

Get the path where the application resides.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
const char * PHYSFS_getBaseDir(void);
```

## Return Value

(const char *) Returns READ ONLY string of base dir in platform-dependent
notation.

## Remarks

Helper function.

Get the "base dir". This is the directory where the application was run
from, which is probably the installation directory, and may or may not be
the process's current working directory.

You should probably use the base dir in your search path.

**WARNING**: On most platforms, this is a directory; on Android, this gives
you the path to the app's package (APK) file. As APK files are just .zip
files, you can mount them in PhysicsFS like regular directories. You'll
probably want to call [PHYSFS_setRoot](PHYSFS_setRoot)(basedir, "/assets")
after mounting to make your app's actual data available directly without
all the Android metadata and directory offset. Note that if you passed a
NULL to [PHYSFS_init](PHYSFS_init)(), you will not get the APK file here.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_getPrefDir](PHYSFS_getPrefDir)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

