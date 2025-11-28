# PHYSFS_setBuffer

Set up buffering for a PhysicsFS file handle.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_setBuffer(PHYSFS_File *handle, PHYSFS_uint64 bufsize);
```

## Function Parameters

|                                |             |                                                     |
| ------------------------------ | ----------- | --------------------------------------------------- |
| [PHYSFS_File](PHYSFS_File) *   | **handle**  | handle returned from [PHYSFS_open](PHYSFS_open)*(). |
| [PHYSFS_uint64](PHYSFS_uint64) | **bufsize** | size, in bytes, of buffer to allocate.              |

## Return Value

(int) Returns nonzero if successful, zero on error.

## Remarks

Define an i/o buffer for a file handle. A memory block of `bufsize` bytes
will be allocated and associated with `handle`.

For files opened for reading, up to `bufsize` bytes are read from `handle`
and stored in the internal buffer. Calls to [PHYSFS_read](PHYSFS_read)()
will pull from this buffer until it is empty, and then refill it for more
reading. Note that compressed files, like ZIP archives, will decompress
while buffering, so this can be handy for offsetting CPU-intensive
operations. The buffer isn't filled until you do your next read.

For files opened for writing, data will be buffered to memory until the
buffer is full or the buffer is flushed. Closing a handle implicitly causes
a flush...check your return values!

Seeking, etc transparently accounts for buffering.

You can resize an existing buffer by calling this function more than once
on the same file. Setting the buffer size to zero will free an existing
buffer.

PhysicsFS file handles are unbuffered by default.

Please check the return value of this function! Failures can include not
being able to seek backwards in a read-only file when removing the buffer,
not being able to allocate the buffer, and not being able to flush the
buffer to disk, among other unexpected problems.

## Thread Safety

Multiple threads can not operate on the same [PHYSFS_File](PHYSFS_File) at
the same time, but they can safely operate on _different_ ones
simultaneously.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_flush](PHYSFS_flush)
- [PHYSFS_read](PHYSFS_read)
- [PHYSFS_write](PHYSFS_write)
- [PHYSFS_close](PHYSFS_close)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

