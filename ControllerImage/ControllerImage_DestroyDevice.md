# ControllerImage_DestroyDevice

Dispose of a previously-created [ControllerImage_Device](ControllerImage_Device) object.

## Header File

Defined in [<controllerimage.h>](https://github.com/icculus/ControllerImage/blob/main/src/controllerimage.h)

## Syntax

```c
void ControllerImage_DestroyDevice(ControllerImage_Device *device);
```

## Function Parameters

|                                                    |            |                           |
| -------------------------------------------------- | ---------- | ------------------------- |
| [ControllerImage_Device](ControllerImage_Device) * | **device** | the object to dispose of. |

## Remarks

Call this once done with a device. Resources are freed and the pointer
passed in here becomes invalid immediately.

## Thread Safety

This function is not thread safe.

## Version

This function is available since ControllerImage 1.0.0.

## See Also

- [ControllerImage_CreateGamepadDevice](ControllerImage_CreateGamepadDevice)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryControllerImage](CategoryControllerImage)

