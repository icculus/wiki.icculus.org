###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_AvailableDecoders

Get a list of sound formats supported by this version of SDL_sound.

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
const Sound_DecoderInfo ** Sound_AvailableDecoders(void);
```

## Return Value

(const [Sound_DecoderInfo](Sound_DecoderInfo) **) Returns READ ONLY
null-terminated array of READ ONLY structures.

## Remarks

This is for informational purposes only. Note that the extension listed is
merely convention: if we list "MP3", you can open an MPEG-1 Layer 3 audio
file with an extension of "XYZ", if you like. The file extensions are
informational, and only required as a hint to choosing the correct decoder,
since the sound data may not be coming from a file at all, thanks to the
abstraction that an SDL_IOStream provides.

The returned value is an array of pointers to
[Sound_DecoderInfo](Sound_DecoderInfo) structures, with a NULL entry to
signify the end of the list:

```c
for (Sound_DecoderInfo **i = Sound_AvailableDecoders(); *i != NULL; i++)
{
    printf("Supported sound format: [%s], which is [%s].\n",
             i->extension, i->description);
    // ...and other fields...
}
```

The return values are pointers to static internal memory, and should be
considered READ ONLY, and never freed.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since SDL_sound 1.0.0.

## See Also

- [Sound_DecoderInfo](Sound_DecoderInfo)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategorySDLSound](CategorySDLSound)

