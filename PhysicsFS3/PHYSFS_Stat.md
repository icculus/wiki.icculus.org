# PHYSFS_Stat

Metadata for a file or directory

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
typedef struct PHYSFS_Stat
{
	PHYSFS_sint64 filesize; /**< size in bytes, -1 for non-files and unknown */
	PHYSFS_sint64 modtime;  /**< last modification time */
	PHYSFS_sint64 createtime; /**< like modtime, but for file creation time */
	PHYSFS_sint64 accesstime; /**< like modtime, but for file access time */
	PHYSFS_FileType filetype; /**< File? Directory? Symlink? */
	int readonly; /**< non-zero if read only, zero if writable. */
} PHYSFS_Stat;
```

## Remarks

Container for various meta data about a file in the virtual file system.
[PHYSFS_stat](PHYSFS_stat)() uses this structure for returning the
information. The time data will be either the number of seconds since the
Unix epoch (midnight, Jan 1, 1970), or -1 if the information isn't
available or applicable. The `filesize` field is measured in bytes. The
`readonly` field tells you whether the archive thinks a file is not
writable, but tends to be only an estimate (for example, your write dir
might overlap with a .zip file, meaning you _can_ successfully open that
path for writing, as it gets created elsewhere.

## Version

This struct is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_stat](PHYSFS_stat)
- [PHYSFS_FileType](PHYSFS_FileType)

----
[CategoryAPI](CategoryAPI), [CategoryAPIStruct](CategoryAPIStruct), [CategoryPhysicsFS](CategoryPhysicsFS)

