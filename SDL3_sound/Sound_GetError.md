###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_GetError

Get the last SDL_sound error message as a null-terminated string.

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
const char * Sound_GetError(void);
```

## Return Value

(const char *) Returns READ ONLY string of last error message.

## Remarks

This will be NULL if there's been no error since the last call to this
function. The pointer returned by this call points to an internal buffer,
and should not be deallocated. Each thread has a unique error state
associated with it, but each time a new error message is set, it will
overwrite the previous one associated with that thread. It is safe to call
this function at anytime, even before [Sound_Init](Sound_Init)().

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since SDL_sound 1.0.0.

## See Also

- [Sound_ClearError](Sound_ClearError)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategorySDLSound](CategorySDLSound)

