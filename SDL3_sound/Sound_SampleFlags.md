###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_SampleFlags

Flags that are used in a [Sound_Sample](Sound_Sample) to show various states.

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
typedef enum Sound_SampleFlags
{
    SOUND_SAMPLEFLAG_NONE    = 0,       /**< No special attributes. */

        /* these are set at sample creation time... */
    SOUND_SAMPLEFLAG_CANSEEK = 1,       /**< Sample can seek to arbitrary points. */

        /* these are set during decoding... */
    SOUND_SAMPLEFLAG_EOF     = 1 << 29, /**< End of input stream. */
    SOUND_SAMPLEFLAG_ERROR   = 1 << 30, /**< Unrecoverable error. */
    SOUND_SAMPLEFLAG_EAGAIN  = 1 << 31  /**< Function would block, or temp error. */
} Sound_SampleFlags;
```

## Version

This enum is available since SDL_sound 1.0.0.

## See Also

- [Sound_SampleNew](Sound_SampleNew)
- [Sound_SampleNewFromFile](Sound_SampleNewFromFile)
- [Sound_SampleDecode](Sound_SampleDecode)
- [Sound_SampleDecodeAll](Sound_SampleDecodeAll)
- [Sound_SampleSeek](Sound_SampleSeek)

----
[CategoryAPI](CategoryAPI), [CategoryAPIEnum](CategoryAPIEnum), [CategorySDLSound](CategorySDLSound)

