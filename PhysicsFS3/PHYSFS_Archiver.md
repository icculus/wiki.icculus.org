# PHYSFS_Archiver

Abstract interface to provide support for user-defined archives.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
typedef struct PHYSFS_Archiver
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
     * Basic info about this archiver.
     *
     * This is used to identify your archive, and is returned in
     * PHYSFS_supportedArchiveTypes().
     */
    PHYSFS_ArchiveInfo info;

    /**
     * Open an archive provided by `io`.
     *
     * This is where resources are allocated and data is parsed when mounting
     * an archive.
     *
     * `name` is a filename associated with `io`, but doesn't necessarily
     * map to anything, let alone a real filename. This possibly-
     * meaningless name is in platform-dependent notation.
     *
     * `forWrite` is non-zero if this is to be used for
     * the write directory, and zero if this is to be used for an
     * element of the search path.
     *
     * `claimed` should be set to 1 if this is definitely an archive your
     * archiver implementation can handle, even if it fails. We use to
     * decide if we should stop trying other archivers if you fail to open
     * it. For example: the .zip archiver will set this to 1 for something
     * that's got a .zip file signature, even if it failed because the file
     * was also truncated. No sense in trying other archivers here, we
     * already tried to handle it with the appropriate implementation!.
     *
     * Returns NULL on failure and set `claimed` appropriately. If no archiver
     * opened the archive or set `claimed`, PHYSFS_mount() will report
     * PHYSFS_ERR_UNSUPPORTED. Otherwise, it will report the error from the
     * archiver that claimed the data through (claimed).
     *
     * Returns non-NULL on success. The pointer returned will be
     * passed as the "opaque" parameter for later calls.
     */
    void *(PHYSFS_CALL *openArchive)(PHYSFS_Io *io, const char *name,
                                     int forWrite, int *claimed);

    /**
     * List all files in (dirname).
     *
     * Each file is passed to `cb`, where a copy is made if appropriate, so
     * you can dispose of it upon return from the callback. `dirname` is in
     * platform-independent notation.
     *
     * If you have a failure, call PHYSFS_SetErrorCode() with whatever code
     * seem appropriate and return PHYSFS_ENUM_ERROR.
     *
     * If the callback returns PHYSFS_ENUM_ERROR, please call
     * PHYSFS_SetErrorCode(PHYSFS_ERR_APP_CALLBACK) and then return
     * PHYSFS_ENUM_ERROR as well. Don't call the callback again in any
     * circumstances.
     *
     * If the callback returns PHYSFS_ENUM_STOP, stop enumerating and return
     * PHYSFS_ENUM_STOP as well. Don't call the callback again in any
     * circumstances. Don't set an error code in this case.
     *
     * Callbacks are only supposed to return a value from
     * PHYSFS_EnumerateCallbackResult. Any other result has undefined
     * behavior.
     *
     * As long as the callback returned PHYSFS_ENUM_OK and you haven't
     * experienced any errors of your own, keep enumerating until you're done
     * and then return PHYSFS_ENUM_OK without setting an error code.
     *
     * **WARNING**: PHYSFS_enumerate returns zero or non-zero (success or failure),
     * so be aware this function pointer returns different values!
     */
    PHYSFS_EnumerateCallbackResult (PHYSFS_CALL *enumerate)(void *opaque,
                     const char *dirname, PHYSFS_EnumerateCallback cb,
                     const char *origdir, void *callbackdata);

    /**
     * Open a file in this archive for reading.
     *
     * This filename, `fnm`, is in platform-independent notation.
     * Fail if the file does not exist.
     *
     * Returns NULL on failure, and calls PHYSFS_setErrorCode().
     *
     * Returns non-NULL on success. The pointer returned will be
     * passed as the "opaque" parameter for later file calls.
     */
    PHYSFS_Io *(PHYSFS_CALL *openRead)(void *opaque, const char *fnm);

    /**
     * Open a file in this archive for writing.
     *
     * If the file does not exist, it should be created. If it exists,
     * it should be truncated to zero bytes. The writing offset should
     * be the start of the file.
     *
     * If the archive is read-only, this operation should fail.
     * This filename is in platform-independent notation.
     *
     * Returns NULL on failure, and calls PHYSFS_setErrorCode().
     *
     * Returns non-NULL on success. The pointer returned will be
     * passed as the "opaque" parameter for later file calls.
     */
    PHYSFS_Io *(PHYSFS_CALL *openWrite)(void *opaque, const char *filename);

    /**
     * Open a file in this archive for appending.
     *
     * If the file does not exist, it should be created. The writing
     * offset should be the end of the file.
     *
     * If the archive is read-only, this operation should fail.
     *
     * This filename is in platform-independent notation.
     *
     * Returns NULL on failure, and calls PHYSFS_setErrorCode().
     *
     * Returns non-NULL on success. The pointer returned will be
     * passed as the "opaque" parameter for later file calls.
     */
    PHYSFS_Io *(PHYSFS_CALL *openAppend)(void *opaque, const char *filename);

    /**
     * Delete a file or directory in the archive.
     *
     * This same call is used for both files and directories; there is not a
     * separate rmdir() call. Directories are only meant to be removed if
     * they are empty.
     *
     * This filename is in platform-independent notation.
     *
     * If the archive is read-only, this operation should fail.
     *
     * Return non-zero on success, zero on failure.
     * On failure, call PHYSFS_setErrorCode().
     */
    int (PHYSFS_CALL *remove)(void *opaque, const char *filename);

    /**
     * Create a directory in the archive.
     *
     * If the application is trying to make multiple dirs, PhysicsFS
     * will split them up into multiple calls before passing them to
     * your driver.
     *
     * This filename is in platform-independent notation.
     *
     * If the archive is read-only, this operation should fail.
     *
     * Return non-zero on success, zero on failure.
     * On failure, call PHYSFS_setErrorCode().
     */
    int (PHYSFS_CALL *mkdir)(void *opaque, const char *filename);

    /**
     * Obtain basic file metadata.
     *
     * On success, fill in all the fields in `stat`, using
     * reasonable defaults for fields that apply to your archive.
     *
     * This filename is in platform-independent notation.
     *
     * Returns non-zero on success, zero on failure.
     * On failure, call PHYSFS_setErrorCode().
     */
    int (PHYSFS_CALL *stat)(void *opaque, const char *fn, PHYSFS_Stat *stat);

    /**
     * Destruct a previously-opened archive.
     *
     * Close this archive, and free any associated memory,
     * including the original PHYSFS_Io and `opaque` itself, if
     * applicable. Implementation can assume that it won't be called if
     * there are still files open from this archive.
     */
    void (PHYSFS_CALL *closeArchive)(void *opaque);
} PHYSFS_Archiver;
```

## Remarks

**WARNING**: This is advanced, hardcore stuff. You don't need this unless
you really know what you're doing. Most apps will not need this.

Historically, PhysicsFS provided a means to mount various archive file
formats, and physical directories in the native filesystem. However,
applications have been limited to the file formats provided by the library.
This interface allows an application to provide their own archive file
types.

Conceptually, a [PHYSFS_Archiver](PHYSFS_Archiver) provides directory
entries, while [PHYSFS_Io](PHYSFS_Io) provides data streams for those
directory entries. The most obvious use of
[PHYSFS_Archiver](PHYSFS_Archiver) is to provide support for an archive
file type that isn't provided by PhysicsFS directly: perhaps some
proprietary format that only your application needs to understand.

Internally, all the built-in archive support uses this interface, so the
best examples for building a [PHYSFS_Archiver](PHYSFS_Archiver) is the
source code to PhysicsFS itself.

An archiver is added to the system with
[PHYSFS_registerArchiver](PHYSFS_registerArchiver)(), and then it will be
available for use automatically with [PHYSFS_mount](PHYSFS_mount)(); if a
given archive can be handled with your archiver, it will be given control
as appropriate.

These methods deal with dir handles. You have one instance of your
archiver, and it generates a unique, opaque handle for each opened archive
in its openArchive() method. Since the lifetime of an Archiver (not an
archive) is generally the entire lifetime of the process, and it's assumed
to be a singleton, we do not provide any instance data for the archiver
itself; the app can just use some static variables if necessary.

Symlinks should always be followed (except in stat()); PhysicsFS will use
the stat() method to check for symlinks and make a judgement on whether to
continue to call other methods based on that.

Archivers, when necessary, should set the PhysicsFS error state with
[PHYSFS_setErrorCode](PHYSFS_setErrorCode)() before returning. PhysicsFS
will pass these errors back to the application unmolested in most cases.

Thread safety: [PHYSFS_Archiver](PHYSFS_Archiver) implementations are not
guaranteed to be thread safe in themselves. PhysicsFS provides thread
safety when it calls into a given archiver inside the library, but it does
not promise that using the same [PHYSFS_File](PHYSFS_File) from two threads
at once is thread-safe; as such, your [PHYSFS_Archiver](PHYSFS_Archiver)
can assume that locking is handled for you so long as the
[PHYSFS_Io](PHYSFS_Io) you return from [PHYSFS_open](PHYSFS_open)* doesn't
change any of your Archiver state, as the [PHYSFS_Io](PHYSFS_Io) won't be
as aggressively protected.

## Version

This struct is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_registerArchiver](PHYSFS_registerArchiver)
- [PHYSFS_deregisterArchiver](PHYSFS_deregisterArchiver)
- [PHYSFS_supportedArchiveTypes](PHYSFS_supportedArchiveTypes)

----
[CategoryAPI](CategoryAPI), [CategoryAPIStruct](CategoryAPIStruct), [CategoryPhysicsFS](CategoryPhysicsFS)

