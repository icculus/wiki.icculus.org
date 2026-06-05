###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_SetDesiredFormat

Change the desired output format for a sample.

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
int Sound_SetDesiredFormat(Sound_Sample *sample, const SDL_AudioSpec *desired);
```

## Function Parameters

|                                |             |                                                                   |
| ------------------------------ | ----------- | ----------------------------------------------------------------- |
| [Sound_Sample](Sound_Sample) * | **sample**  | The [Sound_Sample](Sound_Sample) whose format should be modified. |
| const SDL_AudioSpec *          | **desired** | The new desired format.                                           |

## Return Value

(int) Returns non-zero if format changed, zero on failure.

## Remarks

Future calls to [Sound_Decode](Sound_Decode)() or
[Sound_DecodeAll](Sound_DecodeAll)() will produce audio in the
newly-requested format; SDL_sound will convert on-the-fly while decoding,
if necessary.

The sample's buffer size, must be a multiple of the size of a single sample
frame. If this is no longer the case after the format change, the buffer
size will be reduced by a few bytes to accommodate this, but no actual
reallocation of the buffer is made.
[Sound_SetBufferSize](Sound_SetBufferSize)() can take more explicit control
over the buffer after a format change.

If `desired` is NULL, the sample's actual format is used, disabling audio
conversion.

If this function fails (out of memory setting up a new internal audio
stream, etc), the sample remains usable with its current, unchanged format.

## Thread Safety

It is safe to call this function from any thread, but a single
[Sound_Sample](Sound_Sample) should not be accessed from two threads at the
same time.

## Version

This function is available since SDL_sound 3.0.0.

## See Also

- [Sound_Decode](Sound_Decode)
- [Sound_DecodeAll](Sound_DecodeAll)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategorySDLSound](CategorySDLSound)

