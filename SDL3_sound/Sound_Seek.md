###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_Seek

Seek to a different point in a sample.

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
int Sound_Seek(Sound_Sample *sample, Uint32 ms);
```

## Function Parameters

|                                |            |                                                         |
| ------------------------------ | ---------- | ------------------------------------------------------- |
| [Sound_Sample](Sound_Sample) * | **sample** | the [Sound_Sample](Sound_Sample) to seek.               |
| Uint32                         | **ms**     | the new position, in milliseconds from start of sample. |

## Return Value

(int) Returns nonzero on success, zero on error. Specifics of the error can
be gleaned from [Sound_GetError](Sound_GetError)().

## Remarks

Reposition a sample's stream. If successful, the next call to
[Sound_Decode](Sound_Decode)() or [Sound_DecodeAll](Sound_DecodeAll)() will
give audio data from the offset you specified.

The offset is specified in milliseconds from the start of the sample.

Beware that this function can fail for several reasons. If the SDL_IOStream
that feeds the decoder can not seek, this call will almost certainly fail,
but this can theoretically be avoided by wrapping it in some sort of
buffering SDL_IOStream. Some decoders can never seek, others can only seek
with certain files. The decoders will set a flag in the sample at creation
time to help you determine this.

You should check `sample->flags & SOUND_SAMPLEFLAG_CANSEEK` before
attempting. [Sound_Seek](Sound_Seek)() reports failure immediately if this
flag isn't set. This function can still fail for other reasons if the flag
is set.

This function can be emulated in the application with
[Sound_Rewind](Sound_Rewind)() and predecoding a specific amount of the
sample, but this can be extremely inefficient. [Sound_Seek](Sound_Seek)()
accelerates the seek with decoder-specific code.

If this function fails, the sample should continue to function as if this
call was never made. If there was an unrecoverable error, `sample->flags &
SOUND_SAMPLEFLAG_ERROR` will be set, which your regular decoding loop can
pick up.

On success, [SOUND_SAMPLEFLAG_ERROR](SOUND_SAMPLEFLAG_ERROR),
[SOUND_SAMPLEFLAG_EOF](SOUND_SAMPLEFLAG_EOF), and
[SOUND_SAMPLEFLAG_EAGAIN](SOUND_SAMPLEFLAG_EAGAIN) are cleared from
`sample->flags`.

## Thread Safety

It is safe to call this function from any thread, but a single
[Sound_Sample](Sound_Sample) should not be accessed from two threads at the
same time.

## Version

This function is available since SDL_sound 1.0.0.

## See Also

- [Sound_Rewind](Sound_Rewind)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategorySDLSound](CategorySDLSound)

