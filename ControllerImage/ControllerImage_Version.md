# ControllerImage_Version

Get the version of ControllerImage that is linked against your program.

## Header File

Defined in [<controllerimage.h>](https://github.com/icculus/ControllerImage/blob/main/src/controllerimage.h)

## Syntax

```c
int ControllerImage_Version(void);
```

## Return Value

(int) Returns the version of the linked library.

## Remarks

If you are linking to ControllerImage dynamically, then it is possible that
the current version will be different than the version you compiled
against. This function returns the current version, while
[CONTROLLERIMAGE_VERSION](CONTROLLERIMAGE_VERSION) is the version you
compiled with.

This function may be called safely at any time, even before
[ControllerImage_Init](ControllerImage_Init)().

## Version

This function is available since ControllerImage 1.0.0.

## See Also

- [CONTROLLERIMAGE_VERSION](CONTROLLERIMAGE_VERSION)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryControllerImage](CategoryControllerImage)

