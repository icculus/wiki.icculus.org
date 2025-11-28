# PHYSFS_flush

Flush a buffered PhysicsFS file handle.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_flush(PHYSFS_File *handle);
```

## Function Parameters

|                              |            |                                                     |
| ---------------------------- | ---------- | --------------------------------------------------- |
| [PHYSFS_File](PHYSFS_File) * | **handle** | handle returned from [PHYSFS_open](PHYSFS_open)*(). |

## Return Value

(int) Returns nonzero if successful, zero on error.

## Remarks

For buffered files opened for writing, this will put the current contents
of the buffer to disk and flag the buffer as empty if possible.

For buffered files opened for reading or unbuffered files, this is a safe
no-op, and will report success.

## Thread Safety

Multiple threads can not operate on the same [PHYSFS_File](PHYSFS_File) at
the same time, but they can safely operate on _different_ ones
simultaneously.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_setBuffer](PHYSFS_setBuffer)
- [PHYSFS_close](PHYSFS_close)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

