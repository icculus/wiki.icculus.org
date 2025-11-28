# PHYSFS_getCdRomDirs

Get an array of paths to available CD-ROM drives.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
char ** PHYSFS_getCdRomDirs(void);
```

## Return Value

(char **) Returns Null-terminated array of null-terminated strings.

## Remarks

The dirs returned are platform-dependent ("D:\" on Win32, "/cdrom" or
whatnot on Unix). Dirs are only returned if there is a disc ready and
accessible in the drive. So if you've got two drives (D: and E:), and only
E: has a disc in it, then that's all you get. If the user inserts a disc in
D: and you call this function again, you get both drives. If, on a Unix
box, the user unmounts a disc and remounts it elsewhere, the next call to
this function will reflect that change.

This function refers to "CD-ROM" media, but it really means "inserted disc
media," such as DVD-ROM, HD-DVD, CDRW, and Blu-Ray discs. It looks for
filesystems, and as such won't report an audio CD, unless there's a mounted
filesystem track on it.

The returned value is an array of strings, with a NULL entry to signify the
end of the list:

```c
char **cds = PHYSFS_getCdRomDirs();
for (char **i = cds; *i != NULL; i++) {
    printf("cdrom dir [%s] is available.\n", *i);
}
PHYSFS_freeList(cds);
```

This call may block while drives spin up. Be forewarned.

When you are done with the returned information, you may dispose of the
resources by calling [PHYSFS_freeList](PHYSFS_freeList)() with the returned
pointer.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_getCdRomDirsCallback](PHYSFS_getCdRomDirsCallback)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

