# PHYSFS_getSearchPathCallback

Enumerate the search path, using an application-defined callback.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
void PHYSFS_getSearchPathCallback(PHYSFS_StringCallback c, void *d);
```

## Function Parameters

|                                                |       |                                                           |
| ---------------------------------------------- | ----- | --------------------------------------------------------- |
| [PHYSFS_StringCallback](PHYSFS_StringCallback) | **c** | Callback function to notify about search path elements.   |
| void *                                         | **d** | Application-defined data passed to callback. Can be NULL. |

## Remarks

Internally, [PHYSFS_getSearchPath](PHYSFS_getSearchPath)() just calls this
function and then builds a list before returning to the application, so
functionality is identical except for how the information is represented to
the application.

Unlike [PHYSFS_getSearchPath](PHYSFS_getSearchPath)(), this function does
not return an array. Rather, it calls a function specified by the
application once per element of the search path:

```c *
static void printSearchPath(void *data, const char *pathItem) {
    printf("[%s] is in the search path.\n", pathItem);
}

// ...
PHYSFS_getSearchPathCallback(printSearchPath, NULL);
```

Elements of the search path are reported in order search priority, so the
first archive/dir that would be examined when looking for a file is the
first element passed through the callback.

## Thread Safety

It is safe to call this function from any thread, but this function will
hold a lock that prevents many other PhysicsFS functions from running until
your callback returns and this function finishes. This is only a problem if
you're using this callback to farm work off to other threads that will want
to use PhysicsFS to do work (like enumerating files that another thread
reads in and processes).

## Version

This function is available since PhysicsFS 2.0.0.

## See Also

- [PHYSFS_StringCallback](PHYSFS_StringCallback)
- [PHYSFS_getSearchPath](PHYSFS_getSearchPath)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

