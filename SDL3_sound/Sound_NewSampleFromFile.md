###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_NewSampleFromFile

Start decoding a new sound sample from a file on disk.

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
Sound_Sample * Sound_NewSampleFromFile(const char *filename,
                          const SDL_AudioSpec *desired,
                          Uint32 bufferSize);
```

## Function Parameters

|                       |                |                                                                                       |
| --------------------- | -------------- | ------------------------------------------------------------------------------------- |
| const char *          | **filename**   | file containing sound data.                                                           |
| const SDL_AudioSpec * | **desired**    | Format to convert sound data into. Can usually be NULL, if you don't need conversion. |
| Uint32                | **bufferSize** | size, in bytes, of initial read buffer.                                               |

## Return Value

([Sound_Sample](Sound_Sample) *) Returns [Sound_Sample](Sound_Sample)
pointer, which is used as a handle to several other SDL_sound APIs. NULL on
error. If error, use [Sound_GetError](Sound_GetError)() to see what went
wrong.

## Remarks

This is identical to [Sound_NewSample](Sound_NewSample)(), but it creates
an SDL_IOStream for you from the file located in `filename`. Note that
`filename` is specified in platform-dependent notation.
("C:\\music\\mysong.mp3" on Windows, and "/home/icculus/music/mysong.mp3"
or whatever on Unix, etc.)

[Sound_NewSample](Sound_NewSample)()'s "ext" parameter is gleaned from the
contents of `filename`.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since SDL_sound 1.0.0.

## See Also

- [Sound_NewSample](Sound_NewSample)
- [Sound_SetBufferSize](Sound_SetBufferSize)
- [Sound_Decode](Sound_Decode)
- [Sound_DecodeAll](Sound_DecodeAll)
- [Sound_Seek](Sound_Seek)
- [Sound_Rewind](Sound_Rewind)
- [Sound_FreeSample](Sound_FreeSample)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategorySDLSound](CategorySDLSound)

