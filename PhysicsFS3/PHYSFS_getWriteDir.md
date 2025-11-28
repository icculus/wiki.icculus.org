# PHYSFS_getWriteDir

Get path where PhysicsFS will allow file writing.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
const char * PHYSFS_getWriteDir(void);
```

## Return Value

(const char *) Returns READ ONLY string of write dir in platform-dependent
notation, OR NULL IF NO WRITE PATH IS CURRENTLY SET.

## Remarks

Get the current write dir. The default write dir is NULL.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_setWriteDir](PHYSFS_setWriteDir)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

