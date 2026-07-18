# ControllerImage_GetSVGForAxis

Get the raw SVG data for one axis on a controller.

## Header File

Defined in [<controllerimage.h>](https://github.com/icculus/ControllerImage/blob/main/src/controllerimage.h)

## Syntax

```c
const char * ControllerImage_GetSVGForAxis(ControllerImage_Device *device, SDL_GamepadAxis axis);
```

## Function Parameters

|                                                    |            |                                                      |
| -------------------------------------------------- | ---------- | ---------------------------------------------------- |
| [ControllerImage_Device](ControllerImage_Device) * | **device** | the device object for which to obtain SVG data.      |
| SDL_GamepadAxis                                    | **axis**   | the axis on the device for which to obtain SVG data. |

## Return Value

(const char *) Returns the raw SVG data for the image on success, or NULL
on error; call SDL_GetError() for details.

## Remarks

This can be used if the caller intends to render its own images from
SVG-format data. Most apps will use
[ControllerImage_CreateSurfaceForAxis](ControllerImage_CreateSurfaceForAxis)(),
instead, which will handle generating the pixels internally.

This returns NULL on error, but also if there is no artwork available. For
a controller missing a button, this is not necessarily an error. If the
distinction is important, consider calling
[ControllerImage_DeviceHasArtworkForButton](ControllerImage_DeviceHasArtworkForButton)().

The returned string (SVG files are text-based XML files) is owned by
ControllerImage, not the caller, and should not be free'd. The pointer
remains valid until `device` is destroyed.

## Thread Safety

This function is not thread safe.

## Version

This function is available since ControllerImage 1.0.0.

## See Also

- [ControllerImage_CreateSurfaceForAxis](ControllerImage_CreateSurfaceForAxis)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryControllerImage](CategoryControllerImage)

