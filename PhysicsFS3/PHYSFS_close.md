# PHYSFS_close

Close a PhysicsFS filehandle.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_close(PHYSFS_File *handle);
```

## Function Parameters

|                              |            |                                                     |
| ---------------------------- | ---------- | --------------------------------------------------- |
| [PHYSFS_File](PHYSFS_File) * | **handle** | handle returned from [PHYSFS_open](PHYSFS_open)*(). |

## Return Value

(int) Returns nonzero on success, zero on error. Use
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to obtain the specific
error.

## Remarks

This call is capable of failing if the operating system was buffering
writes to the physical media, and, now forced to write those changes to
physical media, can not store the data for some reason. In such a case, the
filehandle stays open. A well-written program should ALWAYS check the
return value from the close call in addition to every writing call!

## Thread Safety

Multiple threads can not operate on the same [PHYSFS_File](PHYSFS_File) at
the same time, but they can safely operate on _different_ ones
simultaneously.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_openRead](PHYSFS_openRead)
- [PHYSFS_openWrite](PHYSFS_openWrite)
- [PHYSFS_openAppend](PHYSFS_openAppend)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

