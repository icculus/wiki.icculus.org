###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_Quit

Shutdown SDL_sound.

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
int Sound_Quit(void);
```

## Return Value

(int) Returns nonzero on success, zero on error. Specifics of the error can
be gleaned from [Sound_GetError](Sound_GetError)(). If failure, state of
SDL_sound is undefined, and probably badly screwed up.

## Remarks

This closes any SDL_IOStreams that were being used as sound sources, and
frees any resources in use by SDL_sound.

All [Sound_Sample](Sound_Sample) pointers you had prior to this call are
INVALIDATED.

Once successfully deinitialized, [Sound_Init](Sound_Init)() can be called
again to restart the subsystem. All default API states are restored at this
point.

You should call this BEFORE SDL_Quit(). This will NOT call SDL_Quit() for
you!

## Thread Safety

This call is not thread-safe.

## Version

This function is available since SDL_sound 1.0.0.

## See Also

- [Sound_Init](Sound_Init)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategorySDLSound](CategorySDLSound)

