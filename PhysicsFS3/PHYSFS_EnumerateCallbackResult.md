# PHYSFS_EnumerateCallbackResult

Possible return values from [PHYSFS_EnumerateCallback](PHYSFS_EnumerateCallback).

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
typedef enum PHYSFS_EnumerateCallbackResult
{
    PHYSFS_ENUM_ERROR = -1,   /**< Stop enumerating, report error to app. */
    PHYSFS_ENUM_STOP = 0,     /**< Stop enumerating, report success to app. */
    PHYSFS_ENUM_OK = 1        /**< Keep enumerating, no problems */
} PHYSFS_EnumerateCallbackResult;
```

## Remarks

These values dictate if an enumeration callback should continue to fire, or
stop (and why it is stopping).

## Version

This enum is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_EnumerateCallback](PHYSFS_EnumerateCallback)
- [PHYSFS_enumerate](PHYSFS_enumerate)

----
[CategoryAPI](CategoryAPI), [CategoryAPIEnum](CategoryAPIEnum), [CategoryPhysicsFS](CategoryPhysicsFS)

