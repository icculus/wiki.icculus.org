# PHYSFS_swapSLE32

Swap littleendian signed 32 to platform's native byte order.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
PHYSFS_sint32 PHYSFS_swapSLE32(PHYSFS_sint32 val);
```

## Function Parameters

|                                |         |                   |
| ------------------------------ | ------- | ----------------- |
| [PHYSFS_sint32](PHYSFS_sint32) | **val** | value to convert. |

## Return Value

([PHYSFS_sint32](PHYSFS_sint32)) Returns converted value.

## Remarks

Take a 32-bit signed value in littleendian format and convert it to the
platform's native byte order.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

