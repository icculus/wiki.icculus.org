# ControllerImage_Init

Initialize the ControllerImage library.

## Header File

Defined in [<controllerimage.h>](https://github.com/icculus/ControllerImage/blob/main/src/controllerimage.h)

## Syntax

```c
bool ControllerImage_Init(void);
```

## Return Value

(bool) Returns true on success, false on error; call SDL_GetError() for
details.

## Remarks

This must be successfully called once before (almost) any other
ControllerImage function can be used.

It is safe to call this multiple times; the library will only initialize
once, and won't deinitialize until
[ControllerImage_Quit](ControllerImage_Quit)() has been called a matching
number of times. Extra attempts to init report success.

## Thread Safety

This function is not thread safe.

## Version

This function is available since ControllerImage 1.0.0.

## See Also

- [ControllerImage_Quit](ControllerImage_Quit)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryControllerImage](CategoryControllerImage)

