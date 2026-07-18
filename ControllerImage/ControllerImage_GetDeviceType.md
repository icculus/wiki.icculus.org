# ControllerImage_GetDeviceType

Get the device type for a [ControllerImage_Device](ControllerImage_Device) object.

## Header File

Defined in [<controllerimage.h>](https://github.com/icculus/ControllerImage/blob/main/src/controllerimage.h)

## Syntax

```c
const char * ControllerImage_GetDeviceType(ControllerImage_Device *device);
```

## Function Parameters

|                                                    |            |                             |
| -------------------------------------------------- | ---------- | --------------------------- |
| [ControllerImage_Device](ControllerImage_Device) * | **device** | the device object to query. |

## Return Value

(const char *) Returns a NULL-terminated ASCII string, or NULL on error;
call SDL_GetError() for details.

## Remarks

Device types are short, ASCII strings that describe the controller. The
strings are derived from the artset name, not anything that SDL produces.

Some examples strings this function might return are "xbox360", "ps5",
"joyconpair", "ouya".

Generally speaking, this is _not_ intended to be used to identify
controllers; SDL3 has more robust facilities for this task, and this might
be giving a best guess to controller type anyhow. All this tells you is
what artset was chosen.

## Thread Safety

This function is not thread safe.

## Version

This function is available since ControllerImage 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryControllerImage](CategoryControllerImage)

