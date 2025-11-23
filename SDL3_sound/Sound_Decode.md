###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_Decode

Decode more of the sound data in a [Sound_Sample](Sound_Sample).

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
Uint32 Sound_Decode(Sound_Sample *sample);
```

## Function Parameters

|                                |            |                                                        |
| ------------------------------ | ---------- | ------------------------------------------------------ |
| [Sound_Sample](Sound_Sample) * | **sample** | Do more decoding to this [Sound_Sample](Sound_Sample). |

## Return Value

(Uint32) Returns number of bytes decoded into sample->buffer.

## Remarks

It will decode at most `sample->buffer_size` bytes into `sample->buffer` in
the desired format, and return the number of decoded bytes.

If `sample->buffer_size` bytes could not be decoded, then please refer to
`sample->flags` to determine if this was an end-of-stream or error
condition.

## Thread Safety

It is safe to call this function from any thread, but a single
[Sound_Sample](Sound_Sample) should not be accessed from two threads at the
same time.

## Version

This function is available since SDL_sound 1.0.0.

## See Also

- [Sound_DecodeAll](Sound_DecodeAll)
- [Sound_SetBufferSize](Sound_SetBufferSize)
- [Sound_Seek](Sound_Seek)
- [Sound_Rewind](Sound_Rewind)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategorySDLSound](CategorySDLSound)

