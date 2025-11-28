# PHYSFS_ArchiveInfo

Information on various PhysicsFS-supported archives.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
typedef struct PHYSFS_ArchiveInfo
{
    const char *extension;   /**< Archive file extension: "ZIP", for example. */
    const char *description; /**< Human-readable archive description. */
    const char *author;      /**< Person who did support for this archive. */
    const char *url;         /**< URL related to this archive */
    int supportsSymlinks;    /**< non-zero if archive offers symbolic links. */
} PHYSFS_ArchiveInfo;
```

## Remarks

This structure gives you details on what sort of archives are supported by
this implementation of PhysicsFS. Archives tend to be things like ZIP files
and such.

**WARNING**: Not all binaries are created equal! PhysicsFS can be built
with or without support for various archives. You can check with
[PHYSFS_supportedArchiveTypes](PHYSFS_supportedArchiveTypes)() to see if
your archive type is supported.

## Version

This struct is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_supportedArchiveTypes](PHYSFS_supportedArchiveTypes)
- [PHYSFS_registerArchiver](PHYSFS_registerArchiver)
- [PHYSFS_deregisterArchiver](PHYSFS_deregisterArchiver)

----
[CategoryAPI](CategoryAPI), [CategoryAPIStruct](CategoryAPIStruct), [CategoryPhysicsFS](CategoryPhysicsFS)

