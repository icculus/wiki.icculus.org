# PHYSFS_enumerate

Get a file listing of a search path's directory, using an application-defined callback, with errors reported.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_enumerate(const char *dir, PHYSFS_EnumerateCallback c, void *d);
```

## Function Parameters

|                                                      |         |                                                            |
| ---------------------------------------------------- | ------- | ---------------------------------------------------------- |
| const char *                                         | **dir** | Directory, in platform-independent notation, to enumerate. |
| [PHYSFS_EnumerateCallback](PHYSFS_EnumerateCallback) | **c**   | Callback function to notify about search path elements.    |
| void *                                               | **d**   | Application-defined data passed to callback. Can be NULL.  |

## Return Value

(int) Returns non-zero on success, zero on failure. Use
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to obtain the specific
error. If the callback returns [PHYSFS_ENUM_STOP](PHYSFS_ENUM_STOP) to stop
early, this will be considered success. Callbacks returning
[PHYSFS_ENUM_ERROR](PHYSFS_ENUM_ERROR) will make this function return zero
and set the error code to
[PHYSFS_ERR_APP_CALLBACK](PHYSFS_ERR_APP_CALLBACK).

## Remarks

Internally, [PHYSFS_enumerateFiles](PHYSFS_enumerateFiles)() just calls
this function and then builds a list before returning to the application,
so functionality is identical except for how the information is represented
to the application.

Unlike [PHYSFS_enumerateFiles](PHYSFS_enumerateFiles)(), this function does
not return an array. Rather, it calls a function specified by the
application once per element of the search path:

```c
static PHYSFS_EnumerateCallbackResult printDir(void *data, const char *origdir, const char *fname) {
    printf(" * We've got [%s] in [%s].\n", fname, origdir);
    return PHYSFS_ENUM_OK;  // give me more data, please.
}

// ...
PHYSFS_enumerate("/some/path", printDir, NULL);
```

Items sent to the callback are not guaranteed to be in any order
whatsoever. There is no sorting done at this level, and if you need that,
you should probably use [PHYSFS_enumerateFiles](PHYSFS_enumerateFiles)()
instead, which guarantees alphabetical sorting. This form reports whatever
is discovered in each archive before moving on to the next. Even within one
archive, we can't guarantee what order it will discover data. <em>Any
sorting you find in these callbacks is just pure luck. Do not rely on
it.</em> As this walks the entire list of archives, you may receive
duplicate filenames.

This API and the callbacks themselves are capable of reporting errors.
Prior to this API, callbacks had to accept every enumerated item, even if
they were only looking for a specific thing and wanted to stop after that,
or had a serious error and couldn't alert anyone. Furthermore, if PhysicsFS
itself had a problem (disk error or whatnot), it couldn't report it to the
calling app, it would just have to skip items or stop enumerating outright,
and the caller wouldn't know it had lost some data along the way.

Now the caller can be sure it got a complete data set, and its callback has
control if it wants enumeration to stop early. See the documentation for
[PHYSFS_EnumerateCallback](PHYSFS_EnumerateCallback) for details on how
your callback should behave.

## Thread Safety

It is safe to call this function from any thread, but this function will
hold a lock that prevents many other PhysicsFS functions from running until
your callback returns and this function finishes. This is only a problem if
you're using this callback to farm work off to other threads that will want
to use PhysicsFS to do work (like enumerating files that another thread
reads in and processes).

## Version

This function is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_EnumerateCallback](PHYSFS_EnumerateCallback)
- [PHYSFS_enumerateFiles](PHYSFS_enumerateFiles)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

