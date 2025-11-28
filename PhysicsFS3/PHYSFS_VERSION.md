# PHYSFS_VERSION

Macro to determine PhysicsFS version program was compiled against.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
#define PHYSFS_VERSION(x) \
{ \
    (x)->major = PHYSFS_VER_MAJOR; \
    (x)->minor = PHYSFS_VER_MINOR; \
    (x)->patch = PHYSFS_VER_PATCH; \
}
```

## Macro Parameters

|       |                                                                       |
| ----- | --------------------------------------------------------------------- |
| **x** | A pointer to a [PHYSFS_Version](PHYSFS_Version) struct to initialize. |

## Remarks

This macro fills in a [PHYSFS_Version](PHYSFS_Version) structure with the
version of the library you compiled against. This is determined by what
header the compiler uses. Note that if you dynamically linked the library,
you might have a slightly newer or older version at runtime. That version
can be determined with
[PHYSFS_getLinkedVersion](PHYSFS_getLinkedVersion)(), which, unlike
[PHYSFS_VERSION](PHYSFS_VERSION), is not a macro.

## Thread Safety

It is safe to call this macro from any thread.

## Version

This macro is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_Version](PHYSFS_Version)
- [PHYSFS_getLinkedVersion](PHYSFS_getLinkedVersion)

----
[CategoryAPI](CategoryAPI), [CategoryAPIMacro](CategoryAPIMacro), [CategoryPhysicsFS](CategoryPhysicsFS)

