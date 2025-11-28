# PHYSFS_swapULE16

Swap littleendian unsigned 16 to platform's native byte order.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
PHYSFS_uint16 PHYSFS_swapULE16(PHYSFS_uint16 val);
```

## Function Parameters

|                                |         |                   |
| ------------------------------ | ------- | ----------------- |
| [PHYSFS_uint16](PHYSFS_uint16) | **val** | value to convert. |

## Return Value

([PHYSFS_uint16](PHYSFS_uint16)) Returns converted value.

## Remarks

Take a 16-bit unsigned value in littleendian format and convert it to the
platform's native byte order.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

