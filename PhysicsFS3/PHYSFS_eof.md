# PHYSFS_eof

Check for end-of-file state on a PhysicsFS filehandle.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_eof(PHYSFS_File *handle);
```

## Function Parameters

|                              |            |                                                            |
| ---------------------------- | ---------- | ---------------------------------------------------------- |
| [PHYSFS_File](PHYSFS_File) * | **handle** | handle returned from [PHYSFS_openRead](PHYSFS_openRead)(). |

## Return Value

(int) Returns nonzero if EOF, zero if not.

## Remarks

Determine if the end of file has been reached in a PhysicsFS filehandle.

## Thread Safety

Multiple threads can not operate on the same [PHYSFS_File](PHYSFS_File) at
the same time, but they can safely operate on _different_ ones
simultaneously.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_read](PHYSFS_read)
- [PHYSFS_tell](PHYSFS_tell)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

