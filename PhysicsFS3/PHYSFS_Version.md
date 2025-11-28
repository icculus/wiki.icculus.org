# PHYSFS_Version

Information the version of PhysicsFS in use.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
typedef struct PHYSFS_Version
{
    PHYSFS_uint8 major; /**< major revision */
    PHYSFS_uint8 minor; /**< minor revision */
    PHYSFS_uint8 patch; /**< patchlevel */
} PHYSFS_Version;
```

## Remarks

Represents the library's version as three levels: major revision
(increments with massive changes, additions, and enhancements), minor
revision (increments with backwards-compatible changes to the major
revision), and patchlevel (increments with fixes to the minor revision).

## Version

This struct is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_VERSION](PHYSFS_VERSION)
- [PHYSFS_getLinkedVersion](PHYSFS_getLinkedVersion)

----
[CategoryAPI](CategoryAPI), [CategoryAPIStruct](CategoryAPIStruct), [CategoryPhysicsFS](CategoryPhysicsFS)

