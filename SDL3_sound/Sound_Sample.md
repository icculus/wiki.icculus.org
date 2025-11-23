###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_Sample

Represents sound data in the process of being decoded.

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
typedef struct Sound_Sample
{
    void *opaque;  /**< Internal use only. Don't touch. */
    const Sound_DecoderInfo *decoder;  /**< Decoder used for this sample. */
    SDL_AudioSpec desired;  /**< Desired audio format for conversion. */
    SDL_AudioSpec actual;  /**< Actual audio format of sample. */
    void *buffer;  /**< Decoded sound data lands in here. */
    Uint32 buffer_size;  /**< Current size of (buffer), in bytes (Uint8). */
    Sound_SampleFlags flags;  /**< Flags relating to this sample. */
} Sound_Sample;
```

## Remarks

The [Sound_Sample](Sound_Sample) structure is the heart of SDL_sound. This
holds information about a source of sound data as it is being decoded.
EVERY FIELD IN THIS IS READ-ONLY. Please use the API functions to change
them.

## Version

This struct is available since SDL_sound 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIStruct](CategoryAPIStruct), [CategorySDLSound](CategorySDLSound)

