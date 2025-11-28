# PHYSFS_getLastErrorCode

Get machine-readable error information.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
PHYSFS_ErrorCode PHYSFS_getLastErrorCode(void);
```

## Return Value

([PHYSFS_ErrorCode](PHYSFS_ErrorCode)) Returns Enumeration value that
represents last reported error.

## Remarks

Get the last PhysicsFS error message as an integer value. This will return
[PHYSFS_ERR_OK](PHYSFS_ERR_OK) if there's been no error since the last call
to this function. Each thread has a unique error state associated with it,
but each time a new error message is set, it will overwrite the previous
one associated with that thread. It is safe to call this function at
anytime, even before [PHYSFS_init](PHYSFS_init)().

[PHYSFS_getLastError](PHYSFS_getLastError)() and
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() both reset the same
thread-specific error state. Calling one will wipe out the other's data. If
you need both, call [PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)(),
then pass that value to [PHYSFS_getErrorByCode](PHYSFS_getErrorByCode)().

Generally, applications should only concern themselves with whether a given
function failed; however, if you require more specifics, you can try this
function to glean information, if there's some specific problem you're
expecting and plan to handle. But with most things that involve file
systems, the best course of action is usually to give up, report the
problem to the user, and let them figure out what should be done about it.
For that, you might prefer [PHYSFS_getErrorByCode](PHYSFS_getErrorByCode)()
instead.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_getErrorByCode](PHYSFS_getErrorByCode)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

