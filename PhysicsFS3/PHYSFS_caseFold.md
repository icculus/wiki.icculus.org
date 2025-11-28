# PHYSFS_caseFold

"Fold" a Unicode codepoint to a lowercase equivalent.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_caseFold(const PHYSFS_uint32 from, PHYSFS_uint32 *to);
```

## Function Parameters

|                                      |          |                                                                                                                                   |
| ------------------------------------ | -------- | --------------------------------------------------------------------------------------------------------------------------------- |
| const [PHYSFS_uint32](PHYSFS_uint32) | **from** | The codepoint to fold.                                                                                                            |
| [PHYSFS_uint32](PHYSFS_uint32) *     | **to**   | Buffer to store the folded codepoint values into. This should point to space for at least 3 [PHYSFS_uint32](PHYSFS_uint32) slots. |

## Return Value

(int) Returns The number of codepoints the folding produced. Between 1 and
3.

## Remarks

(This is for limited, hardcore use. If you don't immediately see a need for
it, you can probably ignore this forever.)

This will convert a Unicode codepoint into its lowercase equivalent. Bogus
codepoints and codepoints without a lowercase equivalent will be returned
unconverted.

Note that you might get multiple codepoints in return! The German Eszett,
for example, will fold down to two lowercase latin 's' codepoints. The
theory is that if you fold two strings, one with an Eszett and one with
"SS" down, they will match.

**WARNING**: Anyone that is a student of Unicode knows about the "Turkish
I" problem. This API does not handle it. Assume this one letter in all of
Unicode will definitely fold sort of incorrectly. If you don't know what
this is about, you can probably ignore this problem for most of the planet,
but perfection is impossible.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.1.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

