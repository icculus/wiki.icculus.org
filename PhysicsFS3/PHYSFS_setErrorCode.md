# PHYSFS_setErrorCode

Set the current thread's error code.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
void PHYSFS_setErrorCode(PHYSFS_ErrorCode code);
```

## Function Parameters

|                                      |          |                                                            |
| ------------------------------------ | -------- | ---------------------------------------------------------- |
| [PHYSFS_ErrorCode](PHYSFS_ErrorCode) | **code** | Error code to become the current thread's new error state. |

## Remarks

This lets you set the value that will be returned by the next call to
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)(). This will replace any
existing error code, whether set by your application or internally by
PhysicsFS.

Error codes are stored per-thread; what you set here will not be accessible
to another thread.

Any call into PhysicsFS may change the current error code, so any code you
set here is somewhat fragile, and thus you shouldn't build any serious
error reporting framework on this function. The primary goal of this
function is to allow [PHYSFS_Io](PHYSFS_Io) implementations to set the
error state, which generally will be passed back to your application when
PhysicsFS makes a [PHYSFS_Io](PHYSFS_Io) call that fails internally.

This function doesn't care if the error code is a value known to PhysicsFS
or not (but [PHYSFS_getErrorByCode](PHYSFS_getErrorByCode)() will return
NULL for unknown values). The value will be reported unmolested by
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)().

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)
- [PHYSFS_getErrorByCode](PHYSFS_getErrorByCode)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

