# PHYSFS_swapSBE64

Swap bigendian signed 64 to platform's native byte order.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
PHYSFS_sint64 PHYSFS_swapSBE64(PHYSFS_sint64 val);
```

## Function Parameters

|                                |         |                   |
| ------------------------------ | ------- | ----------------- |
| [PHYSFS_sint64](PHYSFS_sint64) | **val** | value to convert. |

## Return Value

([PHYSFS_sint64](PHYSFS_sint64)) Returns converted value.

## Remarks

Take a 64-bit signed value in bigendian format and convert it to the
platform's native byte order.

**WARNING**: Remember, [PHYSFS_sint64](PHYSFS_sint64) is only 32 bits on
platforms without any sort of 64-bit support.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

