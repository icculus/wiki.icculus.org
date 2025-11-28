# PHYSFS_deinit

Deinitialize the PhysicsFS library.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_deinit(void);
```

## Return Value

(int) Returns nonzero on success, zero on error. Specifics of the error can
be gleaned from [PHYSFS_getLastError](PHYSFS_getLastError)(). If failure,
state of PhysFS is undefined, and probably badly screwed up.

## Remarks

This closes any files opened via PhysicsFS, blanks the search/write paths,
frees memory, and invalidates all of your file handles.

Note that this call can FAIL if there's a file open for writing that
refuses to close (for example, the underlying operating system was
buffering writes to network filesystem, and the fileserver has crashed, or
a hard drive has failed, etc). It is usually best to close all write
handles yourself before calling this function, so that you can gracefully
handle a specific failure.

Once successfully deinitialized, [PHYSFS_init](PHYSFS_init)() can be called
again to restart the subsystem. All default API states are restored at this
point, with the exception of any custom allocator you might have specified,
which survives between initializations.

## Thread Safety

This function is not thread safe.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_init](PHYSFS_init)
- [PHYSFS_isInit](PHYSFS_isInit)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

