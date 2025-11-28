# PHYSFS_delete

Delete a file or directory.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_delete(const char *filename);
```

## Function Parameters

|              |              |                     |
| ------------ | ------------ | ------------------- |
| const char * | **filename** | Filename to delete. |

## Return Value

(int) Returns nonzero on success, zero on error. Use
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to obtain the specific
error.

## Remarks

`filename` is specified in platform-independent notation in relation to the
write dir.

A directory must be empty before this call can delete it.

Deleting a symlink will remove the link, not what it points to, regardless
of whether you "permitSymLinks" or not.

So if you've got the write dir set to "C:\mygame\writedir" and call
[PHYSFS_delete](PHYSFS_delete)("downloads/maps/level1.map") then the file
"C:\mygame\writedir\downloads\maps\level1.map" is removed from the physical
filesystem, if it exists and the operating system permits the deletion.

Note that on Unix systems, deleting a file may be successful, but the
actual file won't be removed until all processes that have an open
filehandle to it (including your program) close their handles.

Chances are, the bits that make up the file still exist, they are just made
available to be written over at a later point. Don't consider this a
security method or anything. :)

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

