# ControllerImage_Device

An opaque datatype representing a game controller's set of images.

## Header File

Defined in [<controllerimage.h>](https://github.com/icculus/ControllerImage/blob/main/src/controllerimage.h)

## Syntax

```c
typedef struct ControllerImage_Device ControllerImage_Device;
```

## Remarks

This collects the images of a single device. An app creates one of these
objects for each gamepad it wants to show iconography for. Generally these
live as long as a gamepad is opened, so images at new resolutions can be
generated as needed.

## Version

This datatype is available since ControllerImage 1.0.0.

## See Also

- [ControllerImage_CreateGamepadDevice](ControllerImage_CreateGamepadDevice)
- [ControllerImage_CreateGamepadDeviceByInstance](ControllerImage_CreateGamepadDeviceByInstance)
- [ControllerImage_CreateGamepadDeviceByIdString](ControllerImage_CreateGamepadDeviceByIdString)

----
[CategoryAPI](CategoryAPI), [CategoryAPIDatatype](CategoryAPIDatatype), [CategoryControllerImage](CategoryControllerImage)

