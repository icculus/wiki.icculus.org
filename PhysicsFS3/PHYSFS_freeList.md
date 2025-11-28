# PHYSFS_freeList

Deallocate resources of lists returned by PhysicsFS.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
void PHYSFS_freeList(void *listVar);
```

## Function Parameters

|        |             |                                                                          |
| ------ | ----------- | ------------------------------------------------------------------------ |
| void * | **listVar** | List of information specified as freeable by this function. May be NULL. |

## Remarks

Certain PhysicsFS functions return lists of information that are
dynamically allocated. Use this function to free those resources.

It is safe to pass a NULL here, but doing so will cause a crash in versions
before PhysicsFS 2.1.0.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_getCdRomDirs](PHYSFS_getCdRomDirs)
- [PHYSFS_enumerateFiles](PHYSFS_enumerateFiles)
- [PHYSFS_getSearchPath](PHYSFS_getSearchPath)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

