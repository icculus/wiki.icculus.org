# PHYSFS_FileType

Possible types of a file.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
typedef enum PHYSFS_FileType
{
	PHYSFS_FILETYPE_REGULAR, /**< a normal file */
	PHYSFS_FILETYPE_DIRECTORY, /**< a directory */
	PHYSFS_FILETYPE_SYMLINK, /**< a symlink */
	PHYSFS_FILETYPE_OTHER /**< something completely different like a device */
} PHYSFS_FileType;
```

## Version

This enum is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_stat](PHYSFS_stat)

----
[CategoryAPI](CategoryAPI), [CategoryAPIEnum](CategoryAPIEnum), [CategoryPhysicsFS](CategoryPhysicsFS)

