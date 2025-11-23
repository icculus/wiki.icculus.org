###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_SetBufferSize

Change the current buffer size for a sample.

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
int Sound_SetBufferSize(Sound_Sample *sample,
                Uint32 new_size);
```

## Function Parameters

|                                |              |                                                          |
| ------------------------------ | ------------ | -------------------------------------------------------- |
| [Sound_Sample](Sound_Sample) * | **sample**   | The [Sound_Sample](Sound_Sample) whose buffer to modify. |
| Uint32                         | **new_size** | The desired size, in bytes, of the new buffer.           |

## Return Value

(int) Returns non-zero if buffer size changed, zero on failure.

## Remarks

If the buffer size could be changed, then the `sample->buffer` and
`sample->buffer_size` fields will reflect that. If they could not be
changed, then your original sample state is preserved. If the buffer is
shrinking, the data at the end of buffer is truncated. If the buffer is
growing, the contents of the new space at the end is undefined until you
decode more into it or initialize it yourself.

The buffer size specified must be a multiple of the size of a single sample
frame. So, if you want 16-bit, stereo samples, then your sample frame size
is (2 channels * 16 bits), or 32 bits per sample, which is four bytes. In
such a case, you could specify 128 or 132 bytes for a buffer, but not 129,
130, or 131 (although in reality, you'll want to specify a MUCH larger
buffer).

## Thread Safety

It is safe to call this function from any thread, but a single
[Sound_Sample](Sound_Sample) should not be accessed from two threads at the
same time.

## Version

This function is available since SDL_sound 1.0.0.

## See Also

- [Sound_Decode](Sound_Decode)
- [Sound_DecodeAll](Sound_DecodeAll)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategorySDLSound](CategorySDLSound)

