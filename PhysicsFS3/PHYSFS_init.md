# PHYSFS_init

Initialize the PhysicsFS library.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_init(const char *argv0);
```

## Function Parameters

|              |           |                                                                                                                                                                                                                                                                                                     |
| ------------ | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| const char * | **argv0** | the argv[0] string passed to your program's mainline, or some other system-specific values. |

## Return Value

(int) Returns nonzero on success, zero on error. Specifics of the error can
be gleaned from [PHYSFS_getLastError](PHYSFS_getLastError)().

## Remarks

This must be called before any other PhysicsFS function.

This should be called prior to any attempts to change your process's
current working directory.

`argv0` may be NULL on most platforms (such as ones without a standard 
main() function), but you should always try to pass something in here
when reasonable. Many Unix-like systems _need_ to pass argv[0] from 
main() in here. However several platforms have special needs:

- On Android, argv0 should be a non-NULL pointer to a
[PHYSFS_AndroidInit](PHYSFS_AndroidInit) struct. This struct must hold a
valid JNIEnv * and a JNI jobject of a Context (either the application
context or the current Activity is fine). Both are cast to a void * so we
don't need jni.h included wherever physfs.h is. PhysicsFS uses these
objects to query some system details. PhysicsFS does not hold a reference
to the JNIEnv or Context past the call to [PHYSFS_init](PHYSFS_init)(). If
you pass a NULL here, [PHYSFS_init](PHYSFS_init) can still succeed, but
[PHYSFS_getBaseDir](PHYSFS_getBaseDir)() and
[PHYSFS_getPrefDir](PHYSFS_getPrefDir)() will be incorrect.
- On Playdate, argv0 should be a non-NULL pointer to a
PlaydateAPI struct. PhysicsFS uses this object for system-level access and
will hold it until [PHYSFS_deinit](PHYSFS_deinit) is called. If you pass a
NULL here, PhysicsFS will crash.
- On libretro, argv0 should be a non-NULL pointer to the
retro_environment_t callback. PhysicsFS will use this callback to get
libretro's virtual file system interface, along with any other related
directory paths.

If `argv0` is NULL, PhysicsFS will attempt to work without it, if possible.

## Thread Safety

This function is not thread safe.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_deinit](PHYSFS_deinit)
- [PHYSFS_isInit](PHYSFS_isInit)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

