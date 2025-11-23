###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_DecoderInfo

[Sound_DecoderInfo](Sound_DecoderInfo) Information about available sound decoders.

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
typedef struct Sound_DecoderInfo
{
    const char **extensions; /**< File extensions, list ends with NULL. */
    const char *description; /**< Human readable description of decoder. */
    const char *author;      /**< "Name Of Author <email@emailhost.dom>" */
    const char *url;         /**< URL specific to this decoder. */
} Sound_DecoderInfo;
```

## Remarks

Each decoder sets up one of these structs, which can be retrieved via the
[Sound_AvailableDecoders](Sound_AvailableDecoders)() function. EVERY FIELD
IN THIS IS READ-ONLY.

The extensions field is a NULL-terminated list of ASCIZ strings. You should
read it like this:

```c
for (const char **ext = info->extensions; *ext != NULL; ext++) {
    printf("   File extension \"%s\"\n", *ext);
}
```

The strings in this struct are generally meant to be human-readable.

## Version

This struct is available since SDL_sound 1.0.0.

## See Also

- [Sound_AvailableDecoders](Sound_AvailableDecoders)

----
[CategoryAPI](CategoryAPI), [CategoryAPIStruct](CategoryAPIStruct), [CategorySDLSound](CategorySDLSound)

