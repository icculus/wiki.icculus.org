# ControllerImage_CreateGamepadDevice

Create an device object to obtain image data for a specific gamepad.

## Header File

Defined in [<controllerimage.h>](https://github.com/icculus/ControllerImage/blob/main/src/controllerimage.h)

## Syntax

```c
ControllerImage_Device * ControllerImage_CreateGamepadDevice(SDL_Gamepad *gamepad);
```

## Function Parameters

|               |             |                               |
| ------------- | ----------- | ----------------------------- |
| SDL_Gamepad * | **gamepad** | an opened SDL gamepad to use. |

## Return Value

([ControllerImage_Device](ControllerImage_Device) *) Returns a new device
object on success, false on error; call SDL_GetError() for details.

## Remarks

Once a device object is created, it can be used to obtain image data,
either as SDL_Surface objects, or raw SVG image format strings.

This function uses an SDL_Gamepad to look up data, which is convenient for
preparing image data for a controller that was just opened. One can also
use
[ControllerImage_CreateGamepadDeviceByInstance](ControllerImage_CreateGamepadDeviceByInstance)()
for gamepads that are not yet opened (or joysticks instead of gamepads),
and
[ControllerImage_CreateGamepadDeviceByIdString](ControllerImage_CreateGamepadDeviceByIdString)()
for looking up by GUID or a standard name string.

When done with the returned device object, dispose of it with
[ControllerImage_DestroyDevice](ControllerImage_DestroyDevice)().

## Thread Safety

This function is not thread safe.

## Version

This function is available since ControllerImage 1.0.0.

## See Also

- [ControllerImage_CreateGamepadDeviceByIdString](ControllerImage_CreateGamepadDeviceByIdString)
- [ControllerImage_CreateGamepadDeviceByInstance](ControllerImage_CreateGamepadDeviceByInstance)
- [ControllerImage_DestroyDevice](ControllerImage_DestroyDevice)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryControllerImage](CategoryControllerImage)

