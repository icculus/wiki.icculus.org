# ControllerImage_DeviceHasArtworkForButton

Check if artwork is available for a given button on a specific device.

## Header File

Defined in [<controllerimage.h>](https://github.com/icculus/ControllerImage/blob/main/src/controllerimage.h)

## Syntax

```c
bool ControllerImage_DeviceHasArtworkForButton(ControllerImage_Device *device, SDL_GamepadButton button);
```

## Function Parameters

|                                                    |            |                                                          |
| -------------------------------------------------- | ---------- | -------------------------------------------------------- |
| [ControllerImage_Device](ControllerImage_Device) * | **device** | the device object to query.                              |
| SDL_GamepadButton                                  | **button** | the button on the device to check for available artwork. |

## Return Value

(bool) Returns true if artwork is available, false otherwise.

## Remarks

Not all devices have all buttons, or perhaps an artset is incomplete. This
function reports if artwork for a specific button is available.

A NULL device or a bogus button value will return false; make sure your
parameters are good to get useful information!

## Thread Safety

This function is not thread safe.

## Version

This function is available since ControllerImage 1.0.0.

## See Also

- [ControllerImage_DeviceHasArtworkForAxis](ControllerImage_DeviceHasArtworkForAxis)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryControllerImage](CategoryControllerImage)

