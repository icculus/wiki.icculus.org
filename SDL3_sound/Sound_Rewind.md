###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_Rewind

Rewind a sample to the start.

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
int Sound_Rewind(Sound_Sample *sample);
```

## Function Parameters

|                                |            |                                             |
| ------------------------------ | ---------- | ------------------------------------------- |
| [Sound_Sample](Sound_Sample) * | **sample** | the [Sound_Sample](Sound_Sample) to rewind. |

## Return Value

(int) Returns nonzero on success, zero on error. Specifics of the error can
be gleaned from [Sound_GetError](Sound_GetError)().

## Remarks

Restart a sample at the start of its waveform data, as if newly created
with [Sound_NewSample](Sound_NewSample)(). If successful, the next call to
[Sound_Decode](Sound_Decode)() or [Sound_DecodeAll](Sound_DecodeAll)() will
give audio data from the earliest point in the stream.

Beware that this function will fail if the SDL_IOStream that feeds the
decoder can not be rewound via SDL_SeekIO(), but this can theoretically be
avoided by wrapping it in some sort of buffering SDL_IOStream.

This function should ONLY fail if the SDL_IOStream is not seekable, or
SDL_sound is not initialized. Both can be controlled by the application,
and thus, it is up to the developer's paranoia to dictate whether this
function's return value need be checked at all.

If this function fails, the state of the sample is undefined, but it is
still safe to call [Sound_FreeSample](Sound_FreeSample)() to dispose of it.

On success, [SOUND_SAMPLEFLAG_ERROR](SOUND_SAMPLEFLAG_ERROR),
[SOUND_SAMPLEFLAG_EOF](SOUND_SAMPLEFLAG_EOF), and
[SOUND_SAMPLEFLAG_EAGAIN](SOUND_SAMPLEFLAG_EAGAIN) are cleared from
`sample->flags`. The [SOUND_SAMPLEFLAG_ERROR](SOUND_SAMPLEFLAG_ERROR) flag
will be set on error.

## Thread Safety

It is safe to call this function from any thread, but a single
[Sound_Sample](Sound_Sample) should not be accessed from two threads at the
same time.

## Version

This function is available since SDL_sound 1.0.0.

## See Also

- [Sound_Seek](Sound_Seek)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategorySDLSound](CategorySDLSound)

