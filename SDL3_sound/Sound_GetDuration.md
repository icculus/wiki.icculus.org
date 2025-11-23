###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_GetDuration

Retrieve total play time of sample, in milliseconds.

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
Sint32 Sound_GetDuration(Sound_Sample *sample);
```

## Function Parameters

|                                |            |                                                                           |
| ------------------------------ | ---------- | ------------------------------------------------------------------------- |
| [Sound_Sample](Sound_Sample) * | **sample** | [Sound_Sample](Sound_Sample) from which to retrieve duration information. |

## Return Value

(Sint32) Returns Sample length in milliseconds, or -1 if duration can't be
determined for any reason.

## Remarks

Report total time length of sample, in milliseconds. This is a fast call.
Duration is calculated during [Sound_NewSample](Sound_NewSample)*, so this
is just an accessor into otherwise opaque data.

Please note that not all formats can determine a total time, some can't be
exact without fully decoding the data, and thus will estimate the duration.
Many decoders will require the ability to seek in the data stream to
calculate this, so even if we can tell you how long an .ogg file will be,
the same data set may fail if it's, say, streamed over an HTTP connection.
Plan accordingly.

Most people won't need this function to just decode and playback, but it
can be useful for informational purposes in, say, a music player's UI.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since SDL_sound 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategorySDLSound](CategorySDLSound)

