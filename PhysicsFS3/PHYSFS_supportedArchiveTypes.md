# PHYSFS_supportedArchiveTypes

Get a list of supported archive types.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
const PHYSFS_ArchiveInfo ** PHYSFS_supportedArchiveTypes(void);
```

## Return Value

(const [PHYSFS_ArchiveInfo](PHYSFS_ArchiveInfo) **) Returns READ ONLY
Null-terminated array of READ ONLY structures.

## Remarks

Get a list of archive types supported by this implementation of PhysicFS.
These are the file formats usable for search path entries. This is for
informational purposes only. Note that the extension listed is merely
convention: if we list "ZIP", you can open a PkZip-compatible archive with
an extension of "XYZ", if you like.

The returned value is an array of pointers to
[PHYSFS_ArchiveInfo](PHYSFS_ArchiveInfo) structures, with a NULL entry to
signify the end of the list:

```c
for (PHYSFS_ArchiveInfo **i = PHYSFS_supportedArchiveTypes(); *i; i++) {
    printf("Supported archive: [%s], which is [%s].\n",
             (*i)->extension, (*i)->description);
}
```

The return values are pointers to internal memory, and should be considered
READ ONLY, and never freed. The returned values are valid until the next
call to [PHYSFS_deinit](PHYSFS_deinit)(),
[PHYSFS_registerArchiver](PHYSFS_registerArchiver)(), or
[PHYSFS_deregisterArchiver](PHYSFS_deregisterArchiver)().

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_registerArchiver](PHYSFS_registerArchiver)
- [PHYSFS_deregisterArchiver](PHYSFS_deregisterArchiver)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

