# PHYSFS_EnumerateCallback

Function signature for callbacks that enumerate and return results.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
typedef PHYSFS_EnumerateCallbackResult (PHYSFS_CALL *PHYSFS_EnumerateCallback)(void *data, const char *origdir, const char *fname);
```

## Function Parameters

|             |                                                                                                                                                                                                                                                                               |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **data**    | User-defined data pointer, passed through from the API that eventually called the callback.                                                                                                                                                                                   |
| **origdir** | A string containing the full path, in platform-independent notation, of the directory containing this file. In most cases, this is the directory on which you requested enumeration, passed in the callback for your convenience.                                             |
| **fname**   | The filename that is being enumerated. It may not be in alphabetical order compared to other callbacks that have fired, and it will not contain the full path. You can recreate the fullpath with $origdir/$fname ... The file can be a subdirectory, a file, a symlink, etc. |

## Return Value

Returns A value from
[PHYSFS_EnumerateCallbackResult](PHYSFS_EnumerateCallbackResult). All other
values are (currently) undefined; don't use them.

## Remarks

This is the same thing as
[PHYSFS_EnumFilesCallback](PHYSFS_EnumFilesCallback) from PhysicsFS 2.0,
except it can return a result from the callback: namely: if you're looking
for something specific, once you find it, you can tell PhysicsFS to stop
enumerating further. This is used with
[PHYSFS_enumerate](PHYSFS_enumerate)(), which we hopefully got right this
time. :)

## Version

This typedef is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_enumerate](PHYSFS_enumerate)
- [PHYSFS_EnumerateCallbackResult](PHYSFS_EnumerateCallbackResult)

----
[CategoryAPI](CategoryAPI), [CategoryAPIDatatype](CategoryAPIDatatype), [CategoryPhysicsFS](CategoryPhysicsFS)

