# PHYSFS_mkdir

Create a directory.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_mkdir(const char *dirName);
```

## Function Parameters

|              |             |                    |
| ------------ | ----------- | ------------------ |
| const char * | **dirName** | New dir to create. |

## Return Value

(int) Returns nonzero on success, zero on error. Use
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to obtain the specific
error.

## Remarks

This is specified in platform-independent notation in relation to the write
dir. All missing parent directories are also created if they don't exist.

So if you've got the write dir set to "C:\mygame\writedir" and call
[PHYSFS_mkdir](PHYSFS_mkdir)("downloads/maps") then the directories
"C:\mygame\writedir\downloads" and "C:\mygame\writedir\downloads\maps" will
be created if possible. If the creation of "maps" fails after we have
successfully created "downloads", then the function leaves the created
directory behind and reports failure.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_delete](PHYSFS_delete)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

