###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_FreeSample

Dispose of a [Sound_Sample](Sound_Sample).

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
void Sound_FreeSample(Sound_Sample *sample);
```

## Function Parameters

|                                |            |                                             |
| ------------------------------ | ---------- | ------------------------------------------- |
| [Sound_Sample](Sound_Sample) * | **sample** | The [Sound_Sample](Sound_Sample) to delete. |

## Remarks

This will also close/dispose of the SDL_IOStream that was used at creation
time, so there's no need to keep a reference to that around. The
[Sound_Sample](Sound_Sample) pointer is invalid after this call, and will
almos certainly result in a crash if you attempt to keep using it.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since SDL_sound 1.0.0.

## See Also

- [Sound_NewSample](Sound_NewSample)
- [Sound_NewSampleFromFile](Sound_NewSampleFromFile)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategorySDLSound](CategorySDLSound)

