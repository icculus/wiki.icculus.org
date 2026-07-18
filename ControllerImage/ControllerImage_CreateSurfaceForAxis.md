# ControllerImage_CreateSurfaceForAxis

Render one of a controller's axis images to an SDL_Surface.

## Header File

Defined in [<controllerimage.h>](https://github.com/icculus/ControllerImage/blob/main/src/controllerimage.h)

## Syntax

```c
SDL_Surface * ControllerImage_CreateSurfaceForAxis(ControllerImage_Device *device, SDL_GamepadAxis axis, int size);
```

## Function Parameters

|                                                    |            |                                                                                                                 |
| -------------------------------------------------- | ---------- | --------------------------------------------------------------------------------------------------------------- |
| [ControllerImage_Device](ControllerImage_Device) * | **device** | the device object for which to generate an image.                                                               |
| SDL_GamepadAxis                                    | **axis**   | the axis on the device for which to generate an image.                                                          |
| int                                                | **size**   | the size, in pixels, that the generated SDL_Surface should be, This size is used for both the width and height. |

## Return Value

(SDL_Surface *) Returns a new surface on success, or NULL on error; call
SDL_GetError() for details.

## Remarks

This creates a new surface with the art for a single axis. The artwork is
stored as scalable vector graphics, so it can be generated at any desired
size and look sharp.

All artwork is generated as a square, so the requested size represents both
the width and height in pixels.

Since this has to allocate and rasterize an image, it's not a fast call,
and should probably be done once, not every frame.

This returns NULL on error, but also if there is no artwork available. For
a controller missing an axis, this is not necessarily an error. If the
distinction is important, consider calling
[ControllerImage_DeviceHasArtworkForAxis](ControllerImage_DeviceHasArtworkForAxis)().

The returned SDL_Surface is owned by the caller, who should call
SDL_DestroySurface() to dispose of it when done with it.

## Thread Safety

This function is not thread safe.

## Version

This function is available since ControllerImage 1.0.0.

## See Also

- [ControllerImage_GetSVGForAxis](ControllerImage_GetSVGForAxis)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryControllerImage](CategoryControllerImage)

