# PHYSFS_StringCallback

Function signature for callbacks that report strings.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
typedef void (PHYSFS_CALL *PHYSFS_StringCallback)(void *data, const char *str);
```

## Function Parameters

|          |                                                                                             |
| -------- | ------------------------------------------------------------------------------------------- |
| **data** | User-defined data pointer, passed through from the API that eventually called the callback. |
| **str**  | The string data about which the callback is meant to inform.                                |

## Remarks

These are used to report a list of strings to an original caller, one
string per callback. All strings are UTF-8 encoded. Functions should not
try to modify or free the string's memory.

These callbacks are used, starting in PhysicsFS 1.1, as an alternative to
functions that would return lists that need to be cleaned up with
[PHYSFS_freeList](PHYSFS_freeList)(). The callback means that the library
doesn't need to allocate an entire list and all the strings up front.

Be aware that promises data ordering in the list versions are not
necessarily so in the callback versions. Check the documentation on
specific APIs, but strings may not be sorted as you expect.

## Version

This typedef is available since PhysicsFS 2.0.0.

## See Also

- [PHYSFS_getCdRomDirsCallback](PHYSFS_getCdRomDirsCallback)
- [PHYSFS_getSearchPathCallback](PHYSFS_getSearchPathCallback)

----
[CategoryAPI](CategoryAPI), [CategoryAPIDatatype](CategoryAPIDatatype), [CategoryPhysicsFS](CategoryPhysicsFS)

