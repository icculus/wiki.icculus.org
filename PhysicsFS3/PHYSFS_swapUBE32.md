# PHYSFS_swapUBE32

Swap bigendian unsigned 32 to platform's native byte order.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
PHYSFS_uint32 PHYSFS_swapUBE32(PHYSFS_uint32 val);
```

## Function Parameters

|                                |         |                   |
| ------------------------------ | ------- | ----------------- |
| [PHYSFS_uint32](PHYSFS_uint32) | **val** | value to convert. |

## Return Value

([PHYSFS_uint32](PHYSFS_uint32)) Returns converted value.

## Remarks

Take a 32-bit unsigned value in bigendian format and convert it to the
platform's native byte order.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

