# PHYSFS_Io

An abstract i/o interface.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
typedef struct PHYSFS_Io
{
    /**
     * Binary compatibility information.
     *
     * This must be set to zero at this time. Future versions of this
     * struct will increment this field, so we know what a given
     * implementation supports. We'll presumably keep supporting older
     * versions as we offer new features, though.
     */
    PHYSFS_uint32 version;

    /**
     * Instance data for this struct.
     *
     * Each instance has a pointer associated with it that can be used to
     * store anything it likes. This pointer is per-instance of the stream,
     * so presumably it will change when calling duplicate(). This can be
     * deallocated during the destroy() method.
     */
    void *opaque;

    /**
     * Read more data.
     *
     * Read `len` bytes from the interface, at the current i/o position, and
     * store them in `buffer`. The current i/o position should move ahead
     * by the number of bytes successfully read.
     *
     * You don't have to implement this; set it to NULL if not implemented.
     * This will only be used if the file is opened for reading. If set to
     * NULL, a default implementation that immediately reports failure will
     * be used.
     *
     * \param io The i/o instance to read from.
     * \param buf The buffer to store data into. It must be at least
     *            `len` bytes long and can't be NULL.
     * \param len The number of bytes to read from the interface.
     * \returns number of bytes read from file, 0 on EOF, -1 if complete
     *          failure.
     */
    PHYSFS_sint64 (PHYSFS_CALL *read)(struct PHYSFS_Io *io, void *buf, PHYSFS_uint64 len);

    /**
     * Write more data.
     *
     * Write `len` bytes from `buffer` to the interface at the current i/o
     * position. The current i/o position should move ahead by the number of
     * bytes successfully written.
     *
     * You don't have to implement this; set it to NULL if not implemented.
     * This will only be used if the file is opened for writing. If set to
     * NULL, a default implementation that immediately reports failure will
     * be used.
     *
     * You are allowed to buffer; a write can succeed here and then later
     * fail when flushing. Note that PHYSFS_setBuffer() may be operating a
     * level above your i/o, so you should usually not implement your
     * own buffering routines.
     *
     * \param io The i/o instance to write to.
     * \param buffer The buffer to read data from. It must be at least
     *               `len` bytes long and can't be NULL.
     * \param len The number of bytes to read from `buffer`.
     * \returns number of bytes written to file, -1 if complete failure.
     */
    PHYSFS_sint64 (PHYSFS_CALL *write)(struct PHYSFS_Io *io, const void *buffer,
                           PHYSFS_uint64 len);

    /**
     * Move i/o position to a given byte offset from start.
     *
     * This method moves the i/o position, so the next read/write will
     * be of the byte at `offset` offset. Seeks past the end of file should
     * be treated as an error condition.
     *
     * \param io The i/o instance to seek.
     * \param offset The new byte offset for the i/o position.
     * \returns non-zero on success, zero on error.
     */
    int (PHYSFS_CALL *seek)(struct PHYSFS_Io *io, PHYSFS_uint64 offset);

    /**
     * Report current i/o position.
     *
     * Return bytes offset, or -1 if you aren't able to determine. A failure
     * will almost certainly be fatal to further use of this stream, so you
     * may not leave this unimplemented.
     *
     * \param io The i/o instance to query.
     * \returns The current byte offset for the i/o position, -1 if unknown.
     */
    PHYSFS_sint64 (PHYSFS_CALL *tell)(struct PHYSFS_Io *io);

    /**
     * Determine size of the i/o instance's dataset.
     *
     * Return number of bytes available in the file, or -1 if you
     * aren't able to determine. A failure will almost certainly be fatal
     * to further use of this stream, so you may not leave this unimplemented.
     *
     * \param io The i/o instance to query.
     * \returns Total size, in bytes, of the dataset.
     */
    PHYSFS_sint64 (PHYSFS_CALL *length)(struct PHYSFS_Io *io);

    /**
     * Duplicate this i/o instance.
     *
     * This needs to result in a full copy of this PHYSFS_Io, that can live
     * completely independently. The copy needs to be able to perform all
     * its operations without altering the original, including either object
     * being destroyed separately (so, for example: they can't share a file
     * handle; they each need their own).
     *
     * The current seek position does not need to be duplicated; the caller
     * is expected to explicitly seek the duplicated object before using it.
     *
     * If you can't duplicate a handle, it's legal to return NULL, but you
     * almost certainly need this functionality if you want to use this to
     * PHYSFS_Io to back an archive.
     *
     * \param io The i/o instance to duplicate.
     * \returns A new instance of `io` that can operate independently.
     */
    struct PHYSFS_Io *(PHYSFS_CALL *duplicate)(struct PHYSFS_Io *io);

    /**
     * Flush resources to media, or wherever.
     *
     * This is the chance to report failure for writes that had claimed
     * success earlier, but still had a chance to actually fail. This method
     * can be NULL if flushing isn't necessary.
     *
     * This function may be called before destroy(), as it can report failure
     * and destroy() can not. It may be called at other times, too.
     *
     * \param io The i/o instance to flush.
     * \returns Zero on error, non-zero on success.
     */
    int (PHYSFS_CALL *flush)(struct PHYSFS_Io *io);

    /**
     * Cleanup and deallocate i/o instance.
     *
     * Free associated resources, including `opaque`, if applicable.
     *
     * This function must always succeed: as such, it returns void. The
     * system may call your flush() method before this. You may report
     * failure there if necessary. This method may still be called if
     * flush() fails, in which case you'll have to abandon unflushed data
     * and other failing conditions and clean up.
     *
     * Once this method is called for a given instance, the system will assume
     * it is unsafe to touch that instance again and will discard any
     * references to it.
     *
     * \param s The i/o instance to destroy.
     */
    void (PHYSFS_CALL *destroy)(struct PHYSFS_Io *io);
} PHYSFS_Io;
```

## Remarks

**WARNING**: This is advanced, hardcore stuff. You don't need this unless
you really know what you're doing. Most apps will not need this.

Historically, PhysicsFS provided access to the physical filesystem and
archives within that filesystem. However, sometimes you need more power
than this. Perhaps you need to provide an archive that is entirely
contained in RAM, or you need to bridge some other file i/o API to
PhysicsFS, or you need to translate the bits (perhaps you have a a standard
.zip file that's encrypted, and you need to decrypt on the fly for the
unsuspecting zip archiver).

A [PHYSFS_Io](PHYSFS_Io) is the interface that Archivers use to get archive
data. Historically, this has mapped to file i/o to the physical filesystem,
but as of PhysicsFS 2.1, applications can provide their own i/o
implementations at runtime.

This interface isn't necessarily a good universal fit for i/o. There are a
few requirements of note:

- They only do blocking i/o (at least, for now).
- They need to be able to duplicate. If you have a file handle from
  fopen(), you need to be able to create a unique clone of it (so we have
  two handles to the same file that can both seek/read/etc without stepping
  on each other).
- They need to know the size of their entire data set.
- They need to be able to seek and rewind on demand.

...in short, you're probably not going to write an HTTP implementation.

## Thread Safety

[PHYSFS_Io](PHYSFS_Io) implementations are not guaranteed to be thread safe
in themselves. Under the hood where PhysicsFS uses them, the library
provides its own locks. If you plan to use them directly from separate
threads, you should either use mutexes to protect them, or don't use the
same [PHYSFS_Io](PHYSFS_Io) from two threads at the same time.

## Version

This struct is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_mountIo](PHYSFS_mountIo)

----
[CategoryAPI](CategoryAPI), [CategoryAPIStruct](CategoryAPIStruct), [CategoryPhysicsFS](CategoryPhysicsFS)

