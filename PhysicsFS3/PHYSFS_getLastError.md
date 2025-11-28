# PHYSFS_getLastError

Get human-readable error information.

## Deprecated

Use [PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() and
[PHYSFS_getErrorByCode](PHYSFS_getErrorByCode)() instead.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
const char * PHYSFS_getLastError(void);
```

## Return Value

(const char *) Returns READ ONLY string of last error message.

## Remarks

**WARNING**: As of PhysicsFS 2.1, this function has been nerfed. Before
PhysicsFS 2.1, this function was the only way to get error details beyond a
given function's basic return value. This was meant to be a human-readable
string in one of several languages, and was not useful for application
parsing. This was a problem, because the developer and not the user chose
the language at compile time, and the PhysicsFS maintainers had to (poorly)
maintain a significant amount of localization work. The app couldn't parse
the strings, even if they counted on a specific language, since some were
dynamically generated. In 2.1 and later, this always returns a static
string in English; you may use it as a key string for your own
localizations if you like, as we'll promise not to change existing error
strings. Also, if your application wants to look at specific errors, we now
offer a better option: use
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() instead.

Get the last PhysicsFS error message as a human-readable, null-terminated
string. This will return NULL if there's been no error since the last call
to this function. The pointer returned by this call points to an internal
buffer. Each thread has a unique error state associated with it, but each
time a new error message is set, it will overwrite the previous one
associated with that thread. It is safe to call this function at anytime,
even before [PHYSFS_init](PHYSFS_init)().

[PHYSFS_getLastError](PHYSFS_getLastError)() and
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() both reset the same
thread-specific error state. Calling one will wipe out the other's data. If
you need both, call [PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)(),
then pass that value to [PHYSFS_getErrorByCode](PHYSFS_getErrorByCode)().

As of PhysicsFS 2.1, this function only presents text in the English
language, but the strings are static, so you can use them as keys into your
own localization dictionary. These strings are meant to be passed on
directly to the user.

Generally, applications should only concern themselves with whether a given
function failed; however, if your code require more specifics, you should
use [PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() instead of this
function.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)
- [PHYSFS_getErrorByCode](PHYSFS_getErrorByCode)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

