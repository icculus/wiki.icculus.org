# PHYSFS_CALL

The calling conventions for PhysicsFS entry points.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
#define PHYSFS_CALL
```

## Remarks

This is currently defined to nothing on all platforms and compilers, having
been added very late into PhysicsFS development. As such, at this time it
means all APIs and callbacks use the compiler's default calling conventions
("cdecl" or whatever).

This is for future expansion, perhaps in PhysicsFS 4.0.

## Version

This macro is available since PhysicsFS 3.3.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIMacro](CategoryAPIMacro), [CategoryPhysicsFS](CategoryPhysicsFS)

