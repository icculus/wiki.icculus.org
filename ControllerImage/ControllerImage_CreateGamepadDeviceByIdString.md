# ControllerImage_CreateGamepadDeviceByIdString

Create an device object to obtain image data from an ID string.

## Header File

Defined in [<controllerimage.h>](https://github.com/icculus/ControllerImage/blob/main/src/controllerimage.h)

## Syntax

```c
ControllerImage_Device * ControllerImage_CreateGamepadDeviceByIdString(const char *str);
```

## Function Parameters

|              |         |                                                   |
| ------------ | ------- | ------------------------------------------------- |
| const char * | **str** | an SDL joystick GUID or a artset name to look up. |

## Return Value

([ControllerImage_Device](ControllerImage_Device) *) Returns a new device
object on success, false on error; call SDL_GetError() for details.

## Remarks

Once a device object is created, it can be used to obtain image data,
either as SDL_Surface objects, or raw SVG image format strings.

This function uses a string to look up data. It can be a specific
joystick's GUID or an artset name (see the directory names in
art/standard/gamepad for a list). The standard strings can be useful if you
always want, generically, the "xbox360" image set or whatnot. One can also
use
[ControllerImage_CreateGamepadDevice](ControllerImage_CreateGamepadDevice)()
for gamepads that are opened, and
[ControllerImage_CreateGamepadDeviceByInstance](ControllerImage_CreateGamepadDeviceByInstance)()
for gamepads that are not yet opened (or joysticks instead of gamepads).

When done with the returned device object, dispose of it with
[ControllerImage_DestroyDevice](ControllerImage_DestroyDevice)().

## Thread Safety

This function is not thread safe.

## Version

This function is available since ControllerImage 1.0.0.

## See Also

- [ControllerImage_CreateGamepadDevice](ControllerImage_CreateGamepadDevice)
- [ControllerImage_CreateGamepadDeviceByInstance](ControllerImage_CreateGamepadDeviceByInstance)
- [ControllerImage_DestroyDevice](ControllerImage_DestroyDevice)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryControllerImage](CategoryControllerImage)

