###### (This function is part of SDL_sound, a separate library from SDL.)
# Sound_NewSample

Start decoding a new sound sample.

## Header File

Defined in [<SDL3_sound/SDL_sound.h>](https://github.com/icculus/SDL_sound/blob/main/include/SDL3_sound/SDL_sound.h)

## Syntax

```c
Sound_Sample * Sound_NewSample(SDL_IOStream *io,
                       const char *ext,
                       const SDL_AudioSpec *desired,
                       Uint32 bufferSize);
```

## Function Parameters

|                       |                |                                                                                       |
| --------------------- | -------------- | ------------------------------------------------------------------------------------- |
| SDL_IOStream *        | **io**         | an SDL_IOStream with sound data.                                                      |
| const char *          | **ext**        | file extension normally associated with a data format. Can usually be NULL.           |
| const SDL_AudioSpec * | **desired**    | format to convert sound data into. Can usually be NULL, if you don't need conversion. |
| Uint32                | **bufferSize** | size, in bytes, to allocate for the decoding buffer.                                  |

## Return Value

([Sound_Sample](Sound_Sample) *) Returns [Sound_Sample](Sound_Sample)
pointer, which is used as a handle to several other SDL_sound APIs. NULL on
error. If error, use [Sound_GetError](Sound_GetError)() to see what went
wrong.

## Remarks

The data is read via an SDL_IOStream structure (see SDL_iostream.h in
SDL3's include directory), so it may be coming from memory, disk, network
stream, etc. The (ext) parameter is merely a hint to determining the
correct decoder; if you specify, for example, "mp3" for an extension, and
one of the decoders lists that as a handled extension, then that decoder is
given first shot at trying to claim the data for decoding. If none of the
extensions match (or the extension is NULL), then every decoder examines
the data to determine if it can handle it, until one accepts it. In such a
case your SDL_IOStream will need to be capable of rewinding to the start of
the stream.

If no decoders can handle the data, a NULL value is returned, and a human
readable error message can be fetched from
[Sound_GetError](Sound_GetError)().

Optionally, a desired audio format can be specified. If the incoming data
is in a different format, SDL_sound will convert it to the desired format
on the fly. Note that this can be an expensive operation, so it may be wise
to convert data before you need to play it back, if possible, or make sure
your data is initially in the format that you need it in. If you don't want
to convert the data, you can specify NULL for a desired format. The
incoming format of the data, preconversion, can be found in the
[Sound_Sample](Sound_Sample) structure.

Note that the raw sound data "decoder" needs you to specify both the
extension "RAW" and a "desired" format, or it will refuse to handle the
data. This is to prevent it from catching all formats unsupported by the
other decoders.

Finally, specify an initial buffer size; this is the number of bytes that
will be allocated to store each read from the sound buffer. The more you
can safely allocate, the more decoding can be done in one block, but the
more resources you have to use up, and the longer each decoding call will
take. Note that different data formats require more or less space to store.
This buffer can be resized later via
[Sound_SetBufferSize](Sound_SetBufferSize)().

The buffer size specified must be a multiple of the size of a single sample
frame. So, if you want 16-bit, stereo samples, then your sample frame size
is (2 channels * 16 bits), or 32 bits per frame, which is four bytes. In
such a case, you could specify 128 or 132 bytes for a buffer, but not 129,
130, or 131 (although in reality, you'll want to specify a MUCH larger
buffer).

When you are done with this [Sound_Sample](Sound_Sample) pointer, you can
dispose of it via [Sound_FreeSample](Sound_FreeSample)().

You do not have to keep a reference to `io` around. If this function
suceeds, it stores `io` internally (and disposes of it during the call to
[Sound_FreeSample](Sound_FreeSample)()). If this function fails, it will
dispose of the SDL_IOStream for you.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since SDL_sound 1.0.0.

## See Also

- [Sound_NewSampleFromFile](Sound_NewSampleFromFile)
- [Sound_SetBufferSize](Sound_SetBufferSize)
- [Sound_Decode](Sound_Decode)
- [Sound_DecodeAll](Sound_DecodeAll)
- [Sound_Seek](Sound_Seek)
- [Sound_Rewind](Sound_Rewind)
- [Sound_FreeSample](Sound_FreeSample)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategorySDLSound](CategorySDLSound)

