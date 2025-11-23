###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_ClearError

Clear the current error message.

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
void Sound_ClearError(void);
```

## Remarks

The next call to [Sound_GetError](Sound_GetError)() after
[Sound_ClearError](Sound_ClearError)() will return NULL.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since SDL_sound 1.0.0.

## See Also

- [Sound_GetError](Sound_GetError)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategorySDLSound](CategorySDLSound)

