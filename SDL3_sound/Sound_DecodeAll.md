###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_DecodeAll

Decode the remainder of the sound data in a [Sound_Sample](Sound_Sample).

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
Uint32 Sound_DecodeAll(Sound_Sample *sample);
```

## Function Parameters

|                                |            |                                                        |
| ------------------------------ | ---------- | ------------------------------------------------------ |
| [Sound_Sample](Sound_Sample) * | **sample** | do all decoding for this [Sound_Sample](Sound_Sample). |

## Return Value

(Uint32) Returns number of bytes decoded into sample->buffer. You should
check sample->flags to see what the current state of the sample is (EOF,
error, read again).

## Remarks

This will dynamically allocate memory for the ENTIRE remaining sample.
`sample->buffer_size` and `sample->buffer` will be updated to reflect the
new buffer. Please refer to sample->flags to determine if the decoding
finished due to an end-of-stream or error condition.

Be aware that sound data can take a large amount of memory, and that this
function may block for quite awhile while processing. Also note that a
streaming source (for example, from a SDL_IOStream that is getting fed from
an Internet radio feed that doesn't end) may fill all available memory
before giving up...be sure to use this on finite sound sources only!

When decoding the sample in its entirety, the work is done one buffer at a
time. That is, sound is decoded in `sample->buffer_size` blocks, and
appended to a continually-growing buffer until the decoding completes. That
means that this function will need enough RAM to hold approximately
`sample->buffer_size` bytes plus the complete decoded sample at most. The
larger your buffer size, the less overhead this function needs, but beware
the possibility of paging to disk. Best to make this user-configurable if
the sample isn't specific and small.

## Thread Safety

It is safe to call this function from any thread, but a single
[Sound_Sample](Sound_Sample) should not be accessed from two threads at the
same time.

## Version

This function is available since SDL_sound 1.0.0.

## See Also

- [Sound_Decode](Sound_Decode)
- [Sound_SetBufferSize](Sound_SetBufferSize)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategorySDLSound](CategorySDLSound)

