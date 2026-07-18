# ControllerImage_CreateGamepadDeviceByInstance

Create an device object to obtain image data for a specific SDL_JoystickID.

## Header File

Defined in [<controllerimage.h>](https://github.com/icculus/ControllerImage/blob/main/src/controllerimage.h)

## Syntax

```c
ControllerImage_Device * ControllerImage_CreateGamepadDeviceByInstance(SDL_JoystickID jsid);
```

## Function Parameters

|                |          |                                      |
| -------------- | -------- | ------------------------------------ |
| SDL_JoystickID | **jsid** | an SDL joystick instance to look up. |

## Return Value

([ControllerImage_Device](ControllerImage_Device) *) Returns a new device
object on success, false on error; call SDL_GetError() for details.

## Remarks

Once a device object is created, it can be used to obtain image data,
either as SDL_Surface objects, or raw SVG image format strings.

This function uses an SDL_JoystickID to look up data, which is convenient
for preparing image data for a controller that hasn't yet been opened, or
perhaps an SDL joystick that doesn't have a real gamepad mapping. One can
also use
[ControllerImage_CreateGamepadDevice](ControllerImage_CreateGamepadDevice)()
for gamepads that are opened, and
[ControllerImage_CreateGamepadDeviceByIdString](ControllerImage_CreateGamepadDeviceByIdString)()
for looking up by GUID or a standard name string.

When done with the returned device object, dispose of it with
[ControllerImage_DestroyDevice](ControllerImage_DestroyDevice)().

## Thread Safety

This function is not thread safe.

## Version

This function is available since ControllerImage 1.0.0.

## See Also

- [ControllerImage_CreateGamepadDevice](ControllerImage_CreateGamepadDevice)
- [ControllerImage_CreateGamepadDeviceByIdString](ControllerImage_CreateGamepadDeviceByIdString)
- [ControllerImage_DestroyDevice](ControllerImage_DestroyDevice)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryControllerImage](CategoryControllerImage)

