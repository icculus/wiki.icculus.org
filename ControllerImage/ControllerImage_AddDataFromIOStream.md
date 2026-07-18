# ControllerImage_AddDataFromIOStream

Add data to the ControllerImage database from an SDL_IOStream.

## Header File

Defined in [<controllerimage.h>](https://github.com/icculus/ControllerImage/blob/main/src/controllerimage.h)

## Syntax

```c
bool ControllerImage_AddDataFromIOStream(SDL_IOStream *io, bool closeio);
```

## Function Parameters

|                |             |                                                    |
| -------------- | ----------- | -------------------------------------------------- |
| SDL_IOStream * | **io**      | a stream to provide database data.                 |
| bool           | **closeio** | if true, automatically close the stream when done. |

## Return Value

(bool) Returns true on success, false on error; call SDL_GetError() for
details.

## Remarks

The library needs a database of controller information to be useful. This
data is external to the library and must be provided by the app. See the
library's documentation on how to build the needed data file from the
provided public domain assets.

This should be called successfully at least once before attempting to
create a [ControllerImage_Device](ControllerImage_Device), as doing so will
fail without data.

It is legal to call this function multiple times. If data for the same
gamepad is added twice, the newer call replaces a previous call's data.
This allows an app to add a "standard" database with ControllerImage's
dataset for wide converage, and override the most popular controllers with
a second, custom dataset to match a game's style more closely.

This function takes the data from an SDL_IOStream. It must be in the format
that the make-controllerimage-data.c program produces. There are also
equivalent functions to load from a memory buffer or a filesystem path.

If `closeio` is true, this function will call `SDL_CloseIO(io)` before
returning, whether the function succeeded or not.

## Thread Safety

This function is not thread safe.

## Version

This function is available since ControllerImage 1.0.0.

## See Also

- [ControllerImage_AddData](ControllerImage_AddData)
- [ControllerImage_AddDataFromFile](ControllerImage_AddDataFromFile)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryControllerImage](CategoryControllerImage)

