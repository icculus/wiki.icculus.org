###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_Init

Initialize SDL_sound.

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
int Sound_Init(void);
```

## Return Value

(int) Returns nonzero on success, zero on error. Specifics of the error can
be gleaned from [Sound_GetError](Sound_GetError)().

## Remarks

This must be called before any other SDL_sound function (except perhaps
[Sound_Version](Sound_Version)()). You should call SDL_Init() before
calling this. [Sound_Init](Sound_Init)() will attempt to call
SDL_Init(SDL_INIT_AUDIO), just in case. This is a safe behaviour, but it
may not configure SDL to your liking by itself.

## Thread Safety

This call is not thread-safe.

## Version

This function is available since SDL_sound 1.0.0.

## See Also

- [Sound_Quit](Sound_Quit)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategorySDLSound](CategorySDLSound)

