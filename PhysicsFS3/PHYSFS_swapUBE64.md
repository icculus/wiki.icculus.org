# PHYSFS_swapUBE64

Swap bigendian unsigned 64 to platform's native byte order.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
PHYSFS_uint64 PHYSFS_swapUBE64(PHYSFS_uint64 val);
```

## Function Parameters

|                                |         |                   |
| ------------------------------ | ------- | ----------------- |
| [PHYSFS_uint64](PHYSFS_uint64) | **val** | value to convert. |

## Return Value

([PHYSFS_uint64](PHYSFS_uint64)) Returns converted value.

## Remarks

Take a 64-bit unsigned value in bigendian format and convert it to the
platform's native byte order.

**WARNING**: Remember, [PHYSFS_uint64](PHYSFS_uint64) is only 32 bits on
platforms without any sort of 64-bit support.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

