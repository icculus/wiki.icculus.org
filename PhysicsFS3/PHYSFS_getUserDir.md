# PHYSFS_getUserDir

Get the path where user's home directory resides.

## Deprecated

As of PhysicsFS 2.1, you probably want
[PHYSFS_getPrefDir](PHYSFS_getPrefDir)().

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
const char * PHYSFS_getUserDir(void);
```

## Return Value

(const char *) Returns READ ONLY string of user dir in platform-dependent
notation.

## Remarks

Helper function.

Get the "user dir". This is meant to be a suggestion of where a specific
user of the system can store files. On Unix, this is her home directory. On
systems with no concept of multiple home directories (MacOS, win95), this
will default to something like "C:\mybasedir\users\username" where
"username" will either be the login name, or "default" if the platform
doesn't support multiple users, either.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_getBaseDir](PHYSFS_getBaseDir)
- [PHYSFS_getPrefDir](PHYSFS_getPrefDir)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

