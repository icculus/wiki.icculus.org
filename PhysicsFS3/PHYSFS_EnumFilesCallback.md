# PHYSFS_EnumFilesCallback

Function signature for callbacks that enumerate files.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
typedef void (PHYSFS_CALL *PHYSFS_EnumFilesCallback)(void *data, const char *origdir, const char *fname);
```

## Function Parameters

|             |                                                                                                                                                                                                                                                                               |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **data**    | User-defined data pointer, passed through from the API that eventually called the callback.                                                                                                                                                                                   |
| **origdir** | A string containing the full path, in platform-independent notation, of the directory containing this file. In most cases, this is the directory on which you requested enumeration, passed in the callback for your convenience.                                             |
| **fname**   | The filename that is being enumerated. It may not be in alphabetical order compared to other callbacks that have fired, and it will not contain the full path. You can recreate the fullpath with $origdir/$fname ... The file can be a subdirectory, a file, a symlink, etc. |

## Remarks

**WARNING**: As of PhysicsFS 2.1, Use
[PHYSFS_EnumerateCallback](PHYSFS_EnumerateCallback) with
[PHYSFS_enumerate](PHYSFS_enumerate)() instead; it gives you more control
over the process.

These are used to report a list of directory entries to an original caller,
one file/dir/symlink per callback. All strings are UTF-8 encoded. Functions
should not try to modify or free any string's memory.

These callbacks are used, starting in PhysicsFS 1.1, as an alternative to
functions that would return lists that need to be cleaned up with
[PHYSFS_freeList](PHYSFS_freeList)(). The callback means that the library
doesn't need to allocate an entire list and all the strings up front.

Be aware that promised data ordering in the list versions are not
necessarily so in the callback versions. Check the documentation on
specific APIs, but strings may not be sorted as you expect and you might
get duplicate strings.

## Version

This typedef is available since PhysicsFS 2.0.0.

## See Also

- [PHYSFS_enumerateFilesCallback](PHYSFS_enumerateFilesCallback)

----
[CategoryAPI](CategoryAPI), [CategoryAPIDatatype](CategoryAPIDatatype), [CategoryPhysicsFS](CategoryPhysicsFS)

