###### (This function is part of SDL_sound, a separate library from SDL.)
# SDL_SOUND_VERSION_ATLEAST

This macro will evaluate to true if compiled with SDL_net at least X.Y.Z.

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
#define SDL_SOUND_VERSION_ATLEAST(X, Y, Z) \
    ((SDL_SOUND_MAJOR_VERSION >= X) && \
     (SDL_SOUND_MAJOR_VERSION > X || SDL_SOUND_MINOR_VERSION >= Y) && \
     (SDL_SOUND_MAJOR_VERSION > X || SDL_SOUND_MINOR_VERSION > Y || SDL_SOUND_MICRO_VERSION >= Z))
```

## Version

This macro is available since SDL_net 3.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIMacro](CategoryAPIMacro), [CategorySDLSound](CategorySDLSound)

