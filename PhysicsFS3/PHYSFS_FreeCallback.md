# PHYSFS_FreeCallback

Function signature for callbacks that free a pointer.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
typedef void (PHYSFS_CALL *PHYSFS_FreeCallback)(void *ptr);
```

## Function Parameters

|         |                      |
| ------- | -------------------- |
| **ptr** | The pointer to free. |

## Remarks

These are used to free/delete/deallocate a pointer in an abstract way.

Prior to PhysicsFS 3.3.0, [PHYSFS_mountMemory](PHYSFS_mountMemory)() had a
function pointer declared inline in the function's signature. This just
moves that declaration to its own typedef, for clarity and documentation
purposes, but programs use the API exactly the same way.

## Version

This typedef is available since PhysicsFS 3.3.0.

## See Also

- [PHYSFS_mountMemory](PHYSFS_mountMemory)

----
[CategoryAPI](CategoryAPI), [CategoryAPIDatatype](CategoryAPIDatatype), [CategoryPhysicsFS](CategoryPhysicsFS)

