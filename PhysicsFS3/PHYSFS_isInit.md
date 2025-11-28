# PHYSFS_isInit

Determine if the PhysicsFS library is initialized.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_isInit(void);
```

## Return Value

(int) Returns non-zero if library is initialized, zero if library is not.

## Remarks

Once [PHYSFS_init](PHYSFS_init)() returns successfully, this will return
non-zero. Before a successful [PHYSFS_init](PHYSFS_init)() and after
[PHYSFS_deinit](PHYSFS_deinit)() returns successfully, this will return
zero. This function is safe to call at any time.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.0.0.

## See Also

- [PHYSFS_init](PHYSFS_init)
- [PHYSFS_deinit](PHYSFS_deinit)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

