# PHYSFS_getPrefDir

Get the user-and-app-specific path where files can be written.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
const char * PHYSFS_getPrefDir(const char *org, const char *app);
```

## Function Parameters

|              |         |                                |
| ------------ | ------- | ------------------------------ |
| const char * | **org** | The name of your organization. |
| const char * | **app** | The name of your application.  |

## Return Value

(const char *) Returns READ ONLY string of user dir in platform-dependent
notation. NULL if there's a problem (creating directory failed, etc).

## Remarks

Helper function.

Get the "pref dir". This is meant to be where users can write personal
files (preferences and save games, etc) that are specific to your
application. This directory is unique per user, per application.

This function will decide the appropriate location in the native
filesystem, create the directory if necessary, and return a string in
platform-dependent notation, suitable for passing to
[PHYSFS_setWriteDir](PHYSFS_setWriteDir)().

On Windows, this might look like: "C:\\Users\\bob\\AppData\\Roaming\\My
Company\\My Program Name"

On Linux, this might look like: "/home/bob/.local/share/My Program Name"

On Mac OS X, this might look like: "/Users/bob/Library/Application
Support/My Program Name"

(etc.)

You should probably use the pref dir for your write dir, and also put it
near the beginning of your search path. Older versions of PhysicsFS offered
only [PHYSFS_getUserDir](PHYSFS_getUserDir)() and left you to figure out
where the files should go under that tree. This finds the correct location
for whatever platform, which not only changes between operating systems,
but also versions of the same operating system.

You specify the name of your organization (if it's not a real organization,
your name or an Internet domain you own might do) and the name of your
application. These should be proper names.

Both the `org` and `app` strings may become part of a directory name, so
please follow these rules:

- Try to use the same org string (including case-sensitivity) for all your
  applications that use this function.
- Always use a unique app string for each one, and make sure it never
  changes for an app once you've decided on it.
- Unicode characters are legal, as long as it's UTF-8 encoded, but...
- ...only use letters, numbers, and spaces. Avoid punctuation like "Game
  Name 2: Bad Guy's Revenge!" ... "Game Name 2" is sufficient.

The pointer returned by this function remains valid until you call this
function again, or call [PHYSFS_deinit](PHYSFS_deinit)(). This is not
necessarily a fast call, though, so you should call this once at startup
and copy the string if you need it.

You should assume the path returned by this function is the only safe place
to write files (and that [PHYSFS_getUserDir](PHYSFS_getUserDir)() and
[PHYSFS_getBaseDir](PHYSFS_getBaseDir)(), while they might be writable, or
even parents of the returned path, aren't where you should be writing
things).

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_getBaseDir](PHYSFS_getBaseDir)
- [PHYSFS_getUserDir](PHYSFS_getUserDir)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

